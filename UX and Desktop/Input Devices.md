# Input Devices

## Touchpad / Kinetic Scrolling

The aim is consistent kinetic scrolling across applications, with a way to adjust speed for different touchpads and touchscreens. The original notes question whether more of that behavior should live in the compositor rather than being implemented separately by applications and toolkits. The proposal also needs to prevent momentum from transferring unexpectedly between windows.

Input passes through libinput, the display/compositor stack, and the application toolkit. The exact responsibilities need to be traced for the target applications before choosing an implementation.

### Momentum algorithm references

The collected PastryKit/iOS discussions describe decay factors of 0.9 and 0.95 per frame. One reconstruction uses 1:1 movement during touch, estimates momentum from pixels divided by swipe time, clamps it to zero below 10 pixels or 0.5 units of time, then multiplies by 0.95 each frame. Those are source descriptions with unspecified timing units, not a verified account of current macOS or iOS behavior. The [imported notes](../Reference/Imported%20Notes.md) preserve the excerpts.

* https://news.ycombinator.com/item?id=39607747
* https://stackoverflow.com/questions/38619717/need-help-dissecting-and-recreating-the-perfect-scroll-easing-based-on-pastrykit
* https://medium.com/homullus/recreating-native-ios-scroll-and-momentum-2906d0d711ad

## Keyboard Shortcuts

### Idea: Modal Keys

* Window key for Window Management
    * Window key: launch overview
    * Window-tab: switch between windows
    * Window-left/right: tiling
    * Window-up/down: minimize/maximize
* Alt key for Environment management (all apps)
    * Alt key: open app view
    * Alt-tab: switch between applications
* Ctrl key for Running Application (control focused app)
    * Ctrl-tab: switch between application tabs
* Caps key for controlling terminal

### Mouse Actions

* Middle Click → Minimize
* Double Click → Maximize

### CLI Interface UI Paradigms

* Space shows Command Palette (on desktop for GUI or in modal-CLI apps)
* Mode displayed on screen

## Gaming Mouse Configuration

    sudo systemctl enable --now ratbagd
* Solaar — included for managing Logitech mice along with libratbagd

## Game Controllers

* 8BitDo Ultimate Software Online — 8BitDo's controller configuration tool (button/stick remapping, profiles, firmware updates), historically Windows/Android-only; the "Online" version is announced as browser-based, which would make it usable from Linux (likely via WebHID/WebUSB) without a native app. Evaluate it alongside the controller udev rules in [Gaming Mode](../Performance/Gaming%20Mode.md).
    * https://www.reddit.com/r/linux/comments/1w0lxdh/8bitdo_announce_ultimate_software_online_to/ — link filed from title/announcement; thread not yet reviewed (Reddit blocks automated fetch). VERIFY whether it needs Chromium/WebHID and whether firmware flashing works from Linux.
