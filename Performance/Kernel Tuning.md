## Preemption

### /etc/kernel/cmdline
    +"preempt=full"

#### 2024-09-07 Note (RESOLVED): PREEMPT_RT merged into mainline Linux 6.12 (Nov 2024)
PREEMPT_RT is now available in mainline. For kernels 6.12+, consider using `preempt=full` with the RT patches enabled rather than just `preempt=full` on a non-RT kernel. This should be the preferred configuration for a desktop distro.

Full/rt vs. voluntary preemption can cause a significant degradation in throughput. But Context from the original discussion minimizes the concern:
"It should be the default in distributions. Exceptions might be worth evaluating for server-specific kernels, but even then I suspect they would find that the throughput penalty is not large enough to make it worth disabling.

Without PREEMPT_RT, nevermind forcibly large audio buffers, Linux hiccups are so severe they can even be visible as on-screen stutter.

PREEMPT_RT makes Linux better than both Windows and MacOS for realtime."
[Link](https://www.phoronix.com/forums/forum/phoronix/latest-phoronix-articles/1490123-linux-very-close-to-enabling-real-time-preempt_rt-support/page2)
[Link](https://lwn.net/Articles/994322/)

### Enable rtkit

	sudo systemctl enable --now rtkit-daemon.service

rtkit-daemon (RealtimeKit) is a D-Bus system service that allows user processes to acquire realtime scheduling priority without being root. It does this safely by limiting the maximum realtime priority and watchdogging processes to prevent system lockups. Required for PipeWire and other audio/media applications to achieve low-latency scheduling.

## Interrupts

### /etc/kernel/cmdline
    +="threadirqs"
    +="rcu_nocbs=all"
    +="rcutree.enable_rcu_lazy=1"
     sdbootutil update-all-entries
[Link](https://lwn.net/Articles/931920/)

### Enable IRQ Balancing
	systemctl enable --now irqbalance.service

## Watchdog

##### /etc/kernel/cmdline
    +="nowatchdog"
    +="nmi_watchdog=0"
      sdbootutil update-all-entries
      
##### /etc/modprobe.d/blacklist.conf
    # Blacklist the Intel TCO Watchdog
	blacklist iTCO_wdt

	# Blacklist the AMD SP5100 TCO Watchdog
	blacklist sp5100_tco

## Split Lock Mitigate

### /etc/sysctl.d/30-splitlock.conf
    kernel.split_lock_mitigate = 0

In some cases, split lock mitigate can slow down performance in some applications and games.  So we turn it off
[Link](https://www.phoronix.com/news/Linux-Splitlock-Hurts-Gaming)
[Link](https://github.com/doitsujin/dxvk/issues/2938)


# Udev
## Udev Rules for Game Controllers

Extra udev rules for game controllers and other devices included out of the box.
https://github.com/ublue-os/packages/tree/main/packages/ublue-os-udev-rules/src/udev-rules.d

## Tick Rate

CONFIG_HZ=1000 — the only option that is *only* tunable at compile time. There is a potential risk of regressions for CPU-intensive applications, but they can be mitigated (and maybe even outperformed) with NO_HZ_FULL. On the other hand, HZ=1000 can improve system responsiveness — most desktop and server applications benefit from this (the largest part of server workloads is I/O bound, more than CPU-bound, so they benefit from a kernel that can react faster at switching tasks), not to mention the benefit for typical end user applications (gaming, live conferencing, multimedia, etc.).

--

## CachyOS Kernel Reference

CachyOS Kernel:
* Uses the BORE scheduler
* Built with clang and ThinLTO
* Profiled with AutoFDO
* Choose between 3 kernel schedulers and various sched-ext schedulers for improved responsiveness
* AMD P-State Improvements
* Latest BBRv3 by Google
* le9uo for significantly improved responsiveness during high memory load
* Up-to-date NTSYNC patchset (used with compatible wine/proton builds)
* Compatibility with T2 MacOS devices via t2linux patches
* Per-core CPU energy usage reading for AMD
* ACS Override and v4l2loopback (virtual camera device for OBS, etc.)
* VHBA module for emulating CD/DVD-ROM devices
* Latest ZSTD patchset
* Various other patches (optimized compiler flags, cryptographic improvements, memory management tweaks)

Architecture targets:
* x86-64-v3: 5%-20% performance uplift compared to x86-64
* x86-64-v4: Substantial performance gains through AVX512 support (workload-dependent)
* Zen 4/5: x86-64-v4 instruction set plus additional extensions