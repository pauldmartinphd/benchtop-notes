# Technicomp Benchtop Linux — Design Notes

Working design and reference notes for **Technicomp Benchtop Linux**, an openSUSE
**Tumbleweed** derivative for supported benchtop/laptop hardware — an immutable,
transactional GNOME desktop with two deliberate departures from stock Aeon: a
verbatim upstream kernel.org **LTS kernel** and **GNOME held at old stable
(n−1)**, both delivered via OBS, with Flatpak for GUI apps and Homebrew for CLI
tooling.

These are notes, not documentation — they capture decisions, open questions, and
reference links as the distro is designed. The build lives in separate repos
(`benchtop-linux`, `benchtop-settings`, `benchtop-patterns`, `kernel-lts`,
`packages`).

## Layout

| Folder | Contents |
|---|---|
| `System Core/` | Distro vision, boot/init, filesystems, drivers & firmware, audio, power, packaged environment |
| `UX and Desktop/` | GNOME configuration & extensions, tablet mode, fonts, theming, input devices |
| `Performance/` | Kernel tuning, memory, storage/IO, network, gaming mode, benchmarking |
| `Security/` | Security architecture, security tools |
| `Networking/` | Network services, driverless printing/scanning, self-hosted services |
| `Applications/` | Application list, terminal/CLI stack, browser configuration |
| `OpenSUSE/` | openSUSE/Aeon-specific configuration notes |
| `Reference/` | Research and documentation links |
| `Distro Build Plan.md` | The NixOS-based "fresh userland, boring core" plan — retained as the long-term architecture target (the Aeon path is the ship-now track) |
| `Scratch.md` | Unsorted working notes and links |

## Not included

The associated vulnerability-divergence research plan is intentionally kept out
of this public repository while unpublished.

## Status & license

Pre-release design notes; everything here is subject to change. No license is
declared yet — treat as all-rights-reserved until a `LICENSE` is added.
