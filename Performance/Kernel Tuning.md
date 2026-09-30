# Kernel tuning

The runtime settings below retain the September 16 corrections. Compile-time choices and alternative kernel projects are recorded separately from those settings. The `+` markers in the command-line notes mean “append this parameter”; they are not literal kernel arguments. `sdbootutil update-all-entries` is a command to run after editing, not part of the command line. Parameters that can also be set outside the kernel command line (sysctl, modprobe.d, systemd configuration) are set there instead.

## Preemption

### /etc/kernel/cmdline

    +"preempt=full"

### Full preemption and PREEMPT_RT

The earlier note favors evaluating PREEMPT_RT for desktop latency. Keep that proposal distinct from the selected `preempt=full` boot parameter: full preemption does not turn a non-RT kernel into a PREEMPT_RT build. The kernel configuration and driver compatibility need to be considered separately. See the [kernel parameter reference](https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html) and [PREEMPT_RT theory of operation](https://www.kernel.org/doc/html/next/core-api/real-time/theory.html).

Full and real-time preemption may trade throughput for latency. The original discussion argued that the tradeoff could be worthwhile; the following is a quoted opinion, not a Benchtop benchmark:
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

##### /etc/sysctl.d/30-watchdog.conf

    # Disable the soft lockup detector
	kernel.soft_watchdog = 0

	# Disable NMI watchdog
	-kernel.nmi_watchdog = 0

##### /etc/modprobe.d/blacklist.conf

    # Blacklist the Intel TCO Watchdog
	blacklist iTCO_wdt

	# Blacklist the AMD SP5100 TCO Watchdog
	blacklist sp5100_tco

	# Blacklist the ACPI/WDAT Watchdog/Timer module
	blacklist wdat_wdt

This action will speed up your boot and shutdown, because one less module is loaded.  Additionally disabling watchdog timers increases performance and lowers power consumption
[Link](https://github.com/CachyOS/CachyOS-Settings/blob/master/usr/lib/modprobe.d/blacklist.conf)
[Link](https://github.com/CachyOS/CachyOS-Settings/blob/master/usr/lib/sysctl.d/70-cachyos-settings.conf)

Note: the `-` in front of kernel.nmi_watchdog tells systemd-sysctl to ignore the error on machines without an NMI watchdog (some VMs)

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

`CONFIG_HZ=1000` is a proposed compile-time choice for responsiveness. The original rationale also suggested evaluating `NO_HZ_FULL` to limit throughput costs. Compare scheduling latency, desktop frame times, and CPU-intensive throughput before attributing a benefit to either setting; the notes contain no Benchtop measurements establishing one.

--

## CachyOS Kernel Reference

The following list was collected as a reference for possible experiments, not as a Benchtop patch set or a verified inventory of the current CachyOS kernel:

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

* x86-64-v3: the source notes cite 5–20% over x86-64; no Benchtop measurement is recorded
* x86-64-v4: Substantial performance gains through AVX512 support (workload-dependent)
* Zen 4/5: x86-64-v4 instruction set plus additional extensions
