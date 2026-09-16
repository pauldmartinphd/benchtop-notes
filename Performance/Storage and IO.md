## I/O Scheduler

BFQ is used for rotational disks and slow removable flash because it prioritizes fairness and interactive latency when individual I/O operations are expensive. Kyber is used for SSDs and NVMe because it provides low-overhead queue management suited to fast multiqueue storage. Since USB SSDs and flash drives both appear as `sd*` devices, non-rotational `sd*` devices default to Kyber, with removable USB media explicitly overridden back to BFQ.

## /etc/udev/rules.d/70-iosched.rules

    # /etc/udev/rules.d/10-iosched.rules

	#
	# Slow storage
	#
	# BFQ prioritizes fairness and interactive latency and is well suited to
	# rotational disks and relatively slow flash media.
	#
	
	# Rotational disks: SATA/SAS/USB HDDs.
	ACTION=="add|change", SUBSYSTEM=="block", ENV{DEVTYPE}=="disk", \
	    ATTR{queue/rotational}=="1", \
	    ATTR{queue/scheduler}="bfq"
	
	# SD/eMMC storage.
	ACTION=="add|change", SUBSYSTEM=="block", ENV{DEVTYPE}=="disk", \
	    KERNEL=="mmcblk*", \
	    ATTR{queue/scheduler}="bfq"
	
	
	#
	# Fast solid-state storage
	#
	# Kyber is a low-overhead scheduler intended for fast multiqueue devices.
	#
	
	# NVMe SSDs.
	ACTION=="add|change", SUBSYSTEM=="block", ENV{DEVTYPE}=="disk", \
	    KERNEL=="nvme*n*", \
	    ATTR{queue/rotational}=="0", \
	    ATTR{queue/scheduler}="kyber"
	
	# Non-rotational SCSI-family devices. This includes SATA SSDs as well as
	# USB-attached SSDs and flash devices, so slow removable USB media is
	# overridden by the following rule.
	ACTION=="add|change", SUBSYSTEM=="block", ENV{DEVTYPE}=="disk", \
	    KERNEL=="sd*", \
	    ATTR{queue/rotational}=="0", \
	    ATTR{queue/scheduler}="kyber"
	
	# Slow/removable USB mass storage.
	#
	# This rule intentionally comes after the generic non-rotational sd* rule.
	# USB SSD/NVMe enclosures normally report removable=0 and retain Kyber;
	# removable USB flash media gets BFQ.
	ACTION=="add|change", SUBSYSTEM=="block", ENV{DEVTYPE}=="disk", \
	    KERNEL=="sd*", SUBSYSTEMS=="usb", ATTR{removable}=="1", \
	    ATTR{queue/scheduler}="bfq"
[Link](https://github.com/pop-os/default-settings/pull/149)

### USB Disks

USB flash drives can have extremely slow write performance, allowing a copy dialog to disappear while data is still being written from the kernel cache. Since a user may reach for and remove the drive within roughly a second of seeing the copy complete, slow removable media should have a small per-device dirty-data limit so the outstanding write tail is kept short. This should not affect USB SSDs or NVMe storage, which should retain normal high-performance writeback behavior.

#### /etc/udev/rules.d/71-removable-writeback.rules
	# Slow removable USB storage can accumulate a large amount of dirty data in
	# the page cache. Limit its per-device dirty budget so userspace cannot get
	# far ahead of the physical device.
	#
	# Do not change the global vm.dirty_* timers here; those would also affect
	# high-performance storage such as NVMe.
	
	ACTION=="add|change", SUBSYSTEM=="block", ENV{DEVTYPE}=="disk", \
	    KERNEL=="sd*", SUBSYSTEMS=="usb", ATTR{removable}=="1", \
	    ATTR{bdi/max_bytes}="8388608", \
	    ATTR{bdi/strict_limit}="1"

## Staggered Spin-Up

### /etc/kernel/cmdline
	+="libahci.ignore_sss=1"

"Some hardware implements staggered spin-up, which causes the OS to probe ATA interfaces serially, which can spin up the drives one-by-one and reduce the peak power usage. This slows down the boot speed, and on most consumer hardware provides no benefits at all since the drives will already spin-up immediately when the power is turned on."
[Arch Wiki](https://wiki.archlinux.org/title/Improving_performance/Boot_process)

## TRIM Timer
    sudo systemctl enable --now fstrim.timer

Note: Many USB-attached SSDs support TRIM/UNMAP via UAS (USB Attached SCSI). Ensure the device is detected as UAS rather than BOT (Bulk-Only Transport):
    lsusb -t   # Check for "Driver=uas"
Note: Some USB-SATA bridges do not pass through TRIM commands. Check with `lsblk --discard` — non-zero values in DISC-GRAN and DISC-MAX columns indicate TRIM support.

## /tmp on tmpfs

For a desktop distro, /tmp on tmpfs (RAM-backed) is generally beneficial: it is fast, automatically cleaned on reboot, and reduces SSD write wear. However, it can consume RAM if applications create large temp files (e.g., video editing, compilation).

Recommendation: Keep /tmp on tmpfs (systemd default) but set a size limit:

##### /etc/fstab
    tmpfs  /tmp  tmpfs  defaults,noatime,size=4G  0  0

If the distro's target workloads involve large temp files (e.g., video encoding), consider disabling tmpfs for /tmp:
    sudo systemctl mask tmp.mount

## Access Times

Use `relatime` as the default mount option (this is already the kernel default since Linux 2.6.30). `relatime` only updates the access time (atime) if the previous atime is older than the modify or change time, or if the previous atime is more than 24 hours old. This reduces write overhead vs. the legacy `atime` behavior while still satisfying applications that depend on atime (e.g., tmpwatch, mutt).

For workloads that never need atime (e.g., build servers, databases), `noatime` eliminates the overhead entirely but can break some tools that depend on it. `relatime` is the safe default for a general-purpose desktop distro.

### /etc/fstab
    # Example: ensure relatime is set (should be default, but be explicit)
    UUID=xxx  /  btrfs  defaults,relatime,compress=zstd  0  0

## Optimal Encryption Sector Size

Modern drives with 4096-byte physical sectors should use a 4096-byte encryption sector size for LUKS to avoid read-modify-write overhead. Fedora 35+ defaults to 4096 for new LUKS volumes on drives that report 4K sectors:

    cryptsetup luksFormat --sector-size 4096 /dev/sdX

Check drive sector size:
    cat /sys/block/sdX/queue/physical_block_size
    cat /sys/block/sdX/queue/logical_block_size

NVMe drives almost universally use 4096-byte or 512-byte logical sectors. When logical=512 but physical=4096, aligning the encryption sector size to 4096 still provides a performance benefit.

Note: This only applies to new LUKS volumes. Existing volumes cannot be migrated without re-encryption.
