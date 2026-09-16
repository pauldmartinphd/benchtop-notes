## Virtual Memory

### /etc/sysctl.d/30-vm-default-settings.conf
    vm.swappiness = 180
    vm.watermark_boost_factor = 0
    vm.watermark_scale_factor = 125
    vm.dirty_bytes = 268435456
    vm.dirty_background_bytes = 134217728
    vm.max_map_count = 2147483642
	vm.page-cluster = 0
[Link](https://github.com/pop-os/default-settings/issues/111), [Link](https://github.com/pop-os/default-settings/pull/172)

Note: vm.swappiness=180 is only appropriate when ZRAM is enabled. With ZRAM, the kernel accepts values 0-200, where values above 100 tell it to prefer ZRAM swap over file cache reclaim. Without ZRAM, the maximum meaningful value is 100. The value of vm.page-cluster=0 disables swap readahead, which is correct for ZRAM since ZRAM pages are not contiguous on disk.

Explanation of key settings:
* vm.watermark_boost_factor=0 — disables watermark boosting which can cause unnecessary reclaim on desktop
* vm.watermark_scale_factor=125 — increases the gap between low and high watermarks to reduce reclaim stalls
* vm.dirty_bytes=268435456 (256MB) — limits dirty page cache before synchronous writeback starts
* vm.dirty_background_bytes=134217728 (128MB) — starts background writeback at 128MB of dirty pages
* vm.max_map_count=2147483642 — maximum number of memory map areas per process; required for some games and applications (e.g., Proton/Wine, Elasticsearch)

#### Note on swappiness for audio workloads:
linuxaudio.org states that vm.swappiness=180 is too high for realtime audio. For audio production, set vm.swappiness=10 in /etc/sysctl.conf and run 'sysctl --system'.

However, in our case, vm.swappiness=180 assumes zram-backed swap, where swap I/O is substantially cheaper than filesystem paging. This differs from traditional realtime-audio recommendations such as `swappiness=10`, which are intended to avoid latency from disk-backed swap. Realtime audio applications should lock latency-critical memory rather than relying on low swappiness to prevent paging.
See https://wiki.linuxaudio.org/wiki/system_configuration#sysctlconf

### Transparent Hugepages

###### /etc/tmpfiles.d/30-thp.conf
	# Write Transparent Huge Pages policy at boot
	# Format: type path mode user group age argument
	w /sys/kernel/mm/transparent_hugepage/enabled       - - - - madvise
	w /sys/kernel/mm/transparent_hugepage/defrag        - - - - defer
	w /sys/kernel/mm/transparent_hugepage/shmem_enabled - - - - advise

Note: there is a lot of debate about these settings. Depending on the workload it can help performance, hurt performance (on memory pressure) or make no difference. `always` is opt-out and `madvise` is opt-in. For gaming you want `always` but for desktop responsiveness you want opt-in because page merging actually results in jitter.

###### 2024-09-07 Note: I think maybe we want 2MB THP to minimize TLB use
See also: https://www.phoronix.com/news/Glibc-malloc-2MB-THP-AArch64

[Kernel Docs](https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html) [Arch Reddit](https://www.reddit.com/r/archlinux/comments/1atueo0/higher_ram_usage_since_kernel_67_and_the_solution/) [Steam Deck](https://github.com/CryoByte33/steam-deck-utilities/blob/main/docs/tweak-explanation.md) [Nelhage](https://blog.nelhage.com/post/transparent-hugepages/) [Evan Jones](https://www.evanjones.ca/hugepages-are-a-good-idea.html) [StackOverflow](https://stackoverflow.com/questions/11543748/why-is-the-page-size-of-linux-x86-4-kb-how-is-that-calculated/50033983#50033983)

### ZRAM Swap (Memory Compression)

	sudo systemctl enable --now zramswap.service

### Default Settings
These are already the default for systemd-zram-service.
	
	#. Amount of memory to use for zram, from 1 to 200.
    PORTION=100
    #. Default to compress with zstd, which has an average compression ratio of 3.37.
    ALGO=zstd
    # Higher values encourage the kernel to be more eager to move pages to swap.
    SWAPPINESS=180

### ZRAM Hibernate

https://github.com/gissf1/zram-hibernate/issues

## Resource Limits

### /etc/security/limits.d/20-audio.conf
	# Realtime scheduling privileges for members of the audio group.
	@audio   -   rtprio   99
	@audio   -   nice    -11

### /etc/security/limits.d/30-memlock.conf
	# Allow processes to lock memory without an RLIMIT_MEMLOCK ceiling.
	*   soft   memlock   unlimited
	*   hard   memlock   unlimited

## MGLRU

##### /etc/tmpfiles.d/30-mglru.conf
	# Enable Multi-Gen LRU at boot and set a mild thrash guard
	w /sys/kernel/mm/lru_gen/enabled    - - - - y
	w /sys/kernel/mm/lru_gen/min_ttl_ms - - - - 1000

## OOM Killer
    systemctl enable --now systemd-oomd.service