# Research Links

## Performance

### System Performance

* https://wiki.archlinux.org/title/Improving_performance
* https://wiki.archlinux.org/title/Gaming#Improving_performance
* https://wiki.archlinux.org/title/sysctl
* https://wiki.archlinux.org/index.php/Hardware_video_acceleration
* https://www.clearlinux.org/clear-linux-documentation/guides/index.html
* https://www.clearlinux.org/clear-linux-documentation/guides/clear/performance.html

### Custom Kernels

* https://liquorix.net/#features
* https://github.com/zen-kernel/zen-kernel/wiki/Detailed-Feature-List
* https://github.com/clearlinux-pkgs/linux/
* https://xanmod.org/
* https://news.ycombinator.com/item?id=46366998

### Distro Default Settings (Reference)

* https://github.com/pop-os/default-settings/
* https://github.com/CachyOS/CachyOS-Settings

## Kernel Documentation

* https://www.kernel.org/doc/html/latest
* https://lwn.net/Kernel/Index/
* https://kernelnewbies.org/
* https://wiki.archlinux.org/title/Kernel_parameters

## Accessibility

* http://fireborn.mataroa.blog/blog/i-want-to-love-linux-it-doesnt-love-me-back-post-1-built-for-control-but-not-for-people/

## Udev Rules Reference

* https://github.com/ublue-os/packages/tree/main/packages/ublue-os-udev-rules/src/udev-rules.d (Disabled)

## Manuals and Documentation

* GNU — https://www.gnu.org/
* Kernel — https://www.kernel.org/
* SystemD — https://systemd.io/
* NetworkManager — https://www.networkmanager.dev/
* BlueZ — https://www.bluez.org/
* Tuned — https://tuned-project.org/
* Pipewire — https://www.pipewire.org/
* Mesa — https://mesa3d.org/
* Freedesktop — https://www.freedesktop.org/

## CoreCtrl

CoreCtrl (https://gitlab.com/corectrl/corectrl) is a GUI tool for controlling CPU and GPU settings on Linux. It provides per-application profiles for:

* CPU frequency governor selection (performance, powersave, schedutil)
* GPU clock speed and voltage control (AMD only — uses sysfs interface)
* Fan curve management (AMD GPUs)

Candidate for per-application power and GPU controls. Packaging and polkit integration need checking for the selected image; this note does not establish a distribution channel.
