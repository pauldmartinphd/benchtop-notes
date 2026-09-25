# Technicomp Benchtop Linux — Build Configuration

Technicomp Benchtop Linux is an immutable GNOME desktop image built with kiwi on the openSUSE Build Service. It is based on openSUSE Tumbleweed. The image is assembled against a tested Tumbleweed snapshot, and each package's source is held in a GitHub repository that the Build Service retrieves automatically through scmsync. Because the image is immutable, the entire package set must resolve as a single unit; when it does, the Build Service produces the image, and the running system is updated afterwards by transactional-update.

## Base distribution

The build uses openSUSE Tumbleweed through the repository `openSUSE:Factory/snapshot`. That repository is the openQA-tested Tumbleweed snapshot, and it provides every package as a real, built binary. A kiwi image build requires real binaries, which is the reason Tumbleweed is used rather than Slowroll.

Slowroll was evaluated first and rejected as a build base. On the Build Service, Slowroll's packages are provided through download-on-demand repositories (`openSUSE:Tumbleweed/slowroll` and `openSUSE:Tumbleweed/slowroll-next`), and image builds cannot install download-on-demand binaries. openSUSE produces its own Slowroll installation image only by first copying the required binaries into a staging project. Building against `openSUSE:Factory/snapshot` avoids that entirely, and it is the same base openSUSE's Aeon image uses, from which this image is derived.

## Source repositories

The build is composed of four public repositories under github.com/TechnicompLabs, each mapping to a single Build Service package.

- `benchtop-settings` builds `tc-benchtop-settings`, a configuration package whose files are installed directly from `Source0` onward, without a tarball.
- `benchtop-patterns` builds `patterns-tc-benchtop`, which produces the metapackage `patterns-tc-benchtop-base`. The image depends on that metapackage.
- `benchtop-branding` builds `tc-benchtop-branding`, the wallpaper, and `distribution-logos-tc-benchtop`, the Technicomp logos, which take the place of openSUSE's `distribution-logos-openSUSE-Tumbleweed` so that openSUSE's boot splash, login screen and icons show them.
- `benchtop-image` builds `tc-benchtop-image`, the kiwi image description. It is an oem, btrfs read-only-snapshot layout derived from Aeon.

Each package is connected to its repository by an scmsync entry in its `_meta`:

```
<scmsync>https://github.com/TechnicompLabs/<repo>#main</scmsync>
```

The image description uses `<source path="obsrepositories:/">` for its repository, so the packages come entirely from the repository paths configured in the project metadata. The base is therefore controlled by the project metadata, and `config.kiwi` contains no repository URLs.

## Build Service project structure

```
home:technicomp:benchtop            # repository openSUSE_Tumbleweed -> path openSUSE:Factory/snapshot
  tc-benchtop-settings
  patterns-tc-benchtop
  tc-benchtop-branding
home:technicomp:benchtop:images     # Type: kiwi; repository openSUSE_Tumbleweed
  tc-benchtop-image                 #   paths: home:technicomp:benchtop/openSUSE_Tumbleweed, openSUSE:Factory/snapshot
```

The image resides in its own subproject because a kiwi build requires `Type: kiwi` in the project configuration, and applying that setting to the base project would interfere with the ordinary RPM builds there.

## Provider preferences

Several capabilities that the package set requires can be satisfied by more than one package. The Build Service reports these as "have choice" and does not choose on its own. They are resolved in the project configuration of `home:technicomp:benchtop:images`:

```
Prefer: helm
Prefer: valkey-compat-redis
Prefer: plymouth-branding-openSUSE
Prefer: openSUSE-release-appliance
Prefer: tik-config-generic
```

`helm` is preferred over `helm3`, the legacy name. `valkey-compat-redis` provides the `redis` capability using Valkey. `plymouth-branding-openSUSE` selects the openSUSE boot-splash branding. `openSUSE-release-appliance` selects the appliance release flavor; it is an interim choice, and the image identifies as openSUSE Tumbleweed until a dedicated `tc-benchtop-release` package is created. `tik-config-generic` selects tik's generic configuration rather than Aeon's.

The logos need no preference line, although openSUSE:Factory's own configuration prefers `distribution-logos-openSUSE-Tumbleweed`: the pattern requires `tc-benchtop-branding`, which requires `distribution-logos-tc-benchtop` by name, and the Build Service resolves such single-provider requirements before it makes any choice, so the `distribution-logos` capability is already provided when a choice would arise.

## Automatic rebuilds

A push to any repository rebuilds its package immediately rather than waiting for the scmsync poll. This is configured with one Build Service workflow token and one organization-level GitHub webhook. The GitHub token requires only the `repo:status` scope, so that the Build Service can report build results back onto the commits.

```
osc token --create --operation workflow --scm-token <GITHUB_PAT>   # prints an id and a secret
```

A single webhook is added under TechnicompLabs -> Settings -> Webhooks, using that id and secret:

- Payload URL: `https://build.opensuse.org/trigger/workflow?id=<id>`
- Content type: `application/json`
- Secret: `<secret>`
- Event: push

Each repository contains a `.obs/workflows.yml` naming its own project and package. The `trigger_services` step makes the Build Service retrieve the pushed commit before it builds; `rebuild_package` would only rebuild the source it already holds:

```yaml
rebuild_on_push:
  steps:
    - trigger_services:
        project: <project>
        package: <package>
  filters:
    event: push
    branches:
      only:
        - main
```

## Common commands

```
osc results home:technicomp:benchtop:images                                    # image status
osc buildinfo home:technicomp:benchtop:images tc-benchtop-image openSUSE_Tumbleweed x86_64 \
  2>&1 | grep -iE "nothing provides|unresolvable|have choice"                   # unmet dependencies or provider choices
osc getbinaries home:technicomp:benchtop:images tc-benchtop-image openSUSE_Tumbleweed x86_64   # download the built image
osc service remoterun home:technicomp:benchtop <package>                        # force scmsync to retrieve source again
osc rebuild <project> <package>                                                 # force a rebuild
osc cat <project> <package> <file>                                             # display the source the Build Service holds
```

## Notes on build behaviour

The image resolves against a single tested Tumbleweed snapshot, so the whole package set is internally consistent at build time. The update cadence is determined by which snapshot the build targets; it currently follows the latest tested Tumbleweed snapshot and can be slowed by pinning to a fixed snapshot.

When a package requires a capability that several packages provide, the build fails with "have choice" until a `Prefer` line selects one. This is expected, and is not a missing-package error.

Commit messages contain no co-author or tooling attribution.

## Current state

The image resolves cleanly against `openSUSE:Factory/snapshot` and builds. Remaining work, in rough order: a `tc-benchtop-release` package to give the system its own identity in place of `openSUSE-release-appliance`; a custom kernel; and, if a slower GNOME is wanted, pinning the build to a fixed Tumbleweed snapshot and advancing it deliberately.
