# GNOME Tablet Mode

The goal is a touch interface with larger controls and workspace behavior suited to a tablet. These notes retain the selected interactions and the extension recipe; extension compatibility needs checking against the GNOME release in the image.

## Settings

* Fly-pie
* Keyboard like iPad
* Increase menu bar size
* Automatic maximize to new desktop
* Bigger close button
* Remove minimize and maximize button
* Remove drag to maximize
* Button to disable tablet mode

## Required Extensions

* [Maximize To Empty Workspace](https://extensions.gnome.org/extension/3100/maximize-to-empty-workspace/) — Moves windows when maximized to an empty workspace so every window has its workspace

* [Auto Activities](https://extensions.gnome.org/extension/5500/auto-activities/) — Automatically opens Activities view when no windows (changed to App Grid)

* [Always Show Titles in Overview](https://extensions.gnome.org/extension/1689/always-show-titles-in-overview/) — Titles appear even without hovering (also enabled always-show close button option)

* [Improved OSK](https://github.com/nick-shmyrev/improved-osk-gnome-ext) — Extra keys on the onscreen keyboard, panel button, resizable; fixes some OSK bugs

* [Custom Hot Corners - Extended](https://extensions.gnome.org/extension/4167/custom-hot-corners-extended/) — Use fallback hot corner triggers:
    * Top left: Toggle Overview - App Grid
    * Bottom left: Previous workspace
    * Bottom right: Next workspace
    * These gestures work by swiping from screen corners to the rest of the screen

https://www.reddit.com/r/gnome/comments/1f2p0ir/tutorial_how_to_make_gnome_good_for_a_x64_tablet/
