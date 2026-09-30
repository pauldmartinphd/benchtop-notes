# Pre-Packaged Environment

## CLI Utilities

* yq: command-line YAML, JSON, XML, CSV and properties processor — https://github.com/mikefarah/yq
* pandoc: command-line document conversion format

## Application management

GNOME Software is the application manager. Bazaar is not needed. Retain Warehouse for Flatpak management and Flatseal for permissions management.

### Flathub Per User

Flathub is added to each user's own Flatpak installation at their first login, so apps from Flathub install per user without an administrator password.  Flathub is not configured system-wide (OpenSUSE's flatpak-remote-flathub is left out of the image): with Flathub in both installations, flatpak asks on every install which one to use.  The service runs once for each user, so a user who removes Flathub does not get it back

##### tcbl-flathub.service (user service)

    flatpak remote-add --user --if-not-exists flathub /usr/share/tc-benchtop-settings/flathub.flatpakrepo

GNOME Software installs Flatpak files opened from outside it (such as the .flatpakref from the Install button on flathub.org) into the user's installation:

    gsettings set org.gnome.software install-bundles-system-wide false

### AppImage backend and AppImageHub

GNOME Software needs an AppImage backend with AppImageHub integration so that users can discover and install AppImages through the same interface as other applications. This is a development requirement, not a feature already implemented in the Benchtop image.

Each AppImage should be installed per user in `~/Applications/`. Installation should generate a `.desktop` entry in `$XDG_DATA_HOME/applications/` (normally `~/.local/share/applications/`) so the application appears in the desktop launcher. The entry should use the application’s name and icon and point to the installed executable through an absolute path, with desktop-entry quoting rules applied. The installer should make the AppImage executable.

Updates should keep the launcher pointed at the installed AppImage. Uninstalling should remove the managed AppImage and its generated launcher. The backend and catalog integration still need implementation and testing.

References: [AppImageHub](https://www.appimagehub.com/) and the [Desktop Entry Specification](https://specifications.freedesktop.org/desktop-entry/latest-single/).

## Additional applications

Use Flatpak and AppImage for GUI applications, with GNOME Software as the application manager, and Homebrew for additional CLI tools. Nix is no longer under consideration.

## Backup

* restic — A modern backup program for your files

## Tailscale and desktop integration

Tailscale status, exit-node selection, and connection controls should be accessible from the GNOME desktop. `tailscaled` manages the tunnel; making NetworkManager ignore that interface is separate from exposing useful desktop controls.

The earlier notes proposed this ignore rule:

### /etc/NetworkManager/conf.d/90-tailscale.conf

    [keyfile]
    unmanaged-devices=interface-name:tailscale*

The [Tailscale quick-settings extension](https://github.com/maxgallup/tailscale-gnome-qs) is a candidate for the UI. The earlier claim that `--netfilter-mode=nodivert` enables NetworkManager integration was incorrect: it changes how Tailscale installs firewall rules. It does not create a NetworkManager connection profile. See [Tailscale’s netfilter documentation](https://tailscale.com/docs/reference/netfilter-modes).

## rclone
Mount nearly any remote storage service onto your local machine; great for multi-machine setups.
