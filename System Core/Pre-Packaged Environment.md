# Pre-Packaged Environment

## CLI Utilities

* yq: command-line YAML, JSON, XML, CSV and properties processor — https://github.com/mikefarah/yq
* pandoc: command-line document conversion format

## Flatpak Management

* Bazaar Application Store
* Warehouse for Flatpak management
* Flatseal (permissions manager)

## Additional applications

Use Flatpak for GUI applications and Homebrew for additional CLI tools. Nix is no longer under consideration.

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
