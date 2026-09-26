# Boot and Init

## Boot Chain

* OpenBMC
* CoreBoot signed BIOS w/ no ME
* UEFI Secure Boot w/ HW root of Trust
* Automatic Disk Unlock or Passphrase
* Plymouth
    * GRUB Proper Resolution
    * Flicker-free Boot
    * Hide Kernel Messages on Sleep/Wake
    * Suppress All Messages

## Quiet Boot with Plymouth

##### /etc/kernel/cmdline

    quiet loglevel=2 systemd.show_status=no splash
    sdbootutil update-all-entries

## Shutdown Timeout

    mkdir -p /etc/systemd/system.conf.d

##### /etc/systemd/system.conf.d/10-shutdown.conf

    # Change default stop time for processes from 90 seconds to 15 seconds
    DefaultTimeoutStopSec=15s

## Auto-Update with Notify

    echo 'REBOOT_METHOD=notify' | sudo tee /etc/transactional-update.conf
    sudo systemctl enable --now transactional-update.timer
    systemctl --user enable --now transactional-update-notifier.service

	sudo install -d -m 0755 /etc/rebootmgr/rebootmgr.conf.d
	printf '[rebootmgr]\nstrategy=off\n' | sudo tee /etc/rebootmgr/rebootmgr.conf.d/50-strategy.conf
	sudo systemctl restart rebootmgr
    sudo systemctl disable --now rebootmgr.service

## DBUS Broker

	systemctl enable dbus-broker.service
    sudo systemctl --global enable dbus-broker.service
Note: I believe this is now OpenSUSE default

## systemd-bsod

systemd-bsod (introduced in systemd 255) displays a full-screen error message on the framebuffer when the system fails to boot. It captures the emergency-level log messages and renders them in a readable format, similar to Windows' blue screen. This replaces the old behavior of dropping to a tiny-font emergency shell that most users cannot read.

To enable:

    sudo systemctl enable systemd-bsod.service

Note: Requires the framebuffer to be available at early boot (i.e., working Plymouth/KMS). On OpenSUSE MicroOS/Aeon, this may already be enabled.

## Linux Resume Quirks

* Reset Bluetooth
* Reset WiFi
* Reset Trackpad
* Reset Touchscreen

## Flicker-free Boot

A flicker-free boot requires the entire chain from firmware to desktop to maintain the same display mode without any mode-setting transitions:

1. Firmware (UEFI GOP) sets the native resolution
2. GRUB/systemd-boot must not change the video mode — use `GRUB_GFXMODE=auto` or systemd-boot with `console-mode auto`
3. Kernel must use early KMS (Kernel Mode Setting) — the GPU driver must be built into the initramfs, not loaded as a module later
4. Plymouth must use the DRM (direct rendering) backend, not the fbdev fallback

##### /etc/kernel/cmdline (already set in Quiet Boot section)

    quiet loglevel=2 systemd.show_status=no splash

##### /etc/dracut.conf.d/10-early-kms.conf

    # Force GPU driver into initramfs for early KMS
    # For Intel:
    force_drivers+=" i915 "
    # For AMD:
    force_drivers+=" amdgpu "
    # For NVIDIA (open kernel module):
    force_drivers+=" nvidia nvidia_modeset nvidia_uvm nvidia_drm "

Rebuild initramfs after changes:

    sudo dracut --force

## Hide Kernel Messages on Sleep/Wake

Kernel messages during suspend/resume break the visual experience. To suppress them:

##### /etc/kernel/cmdline

    quiet loglevel=0

`loglevel=0` suppresses normal console printing, including KERN_EMERG at level 0: a message is normally printed only when its numeric priority is lower than the console threshold. See the [kernel printk documentation](https://cdn.kernel.org/doc/html/latest/core-api/printk-basics.html). Use `loglevel=2` during development and `loglevel=0` for the final distro image. Alternatively, keep `loglevel=2` and rely on Plymouth to mask the console output visually during suspend/resume transitions.
