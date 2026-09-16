## Performance Tools and Applications

* [GameMode](https://github.com/FeralInteractive/gamemode/) — Feral Interactive's on-demand game optimizer
* [system76-scheduler](https://github.com/pop-os/system76-scheduler) — Process priority scheduling
* [MangoHUD](https://mangohud.com/) — Vulkan/OpenGL overlay for monitoring FPS, temps, etc.
* [LACT](https://github.com/ilya-zlobintsev/LACT) — Linux GPU Configuration Tool
* [CPU-X](https://thetumultuousunicornofdarkness.github.io/CPU-X/) — CPU/GPU/motherboard info
* [hardinfo2](https://github.com/hardinfo2/hardinfo2) — System profiler and benchmark

## Other Performance Applications

* [Preload](https://wiki.archlinux.org/title/Preload) — Adaptive readahead daemon
* ~~[Prelink](https://handwiki.org/wiki/Prelink)~~ — ELF prelinking (DEPRECATED: Prelink is no longer maintained and is incompatible with modern security features like ASLR and PIE. Do not use.)
* [Ananicy-cpp](https://gitlab.com/ananicy-cpp/ananicy-cpp) — Auto nice daemon (note: the original [Ananicy](https://github.com/Nefelim4ag/Ananicy) in Python is abandoned; use the C++ rewrite instead)
* [nohang](https://github.com/hakavlad/nohang) — OOM prevention daemon
* [auto-cpufreq](https://github.com/AdnanHodzic/auto-cpufreq) — Automatic CPU speed/power optimizer
* [bpftune](https://github.com/oracle/bpftune) — BPF-driven auto-tuning
* [zorin-exec-guard](https://github.com/ZorinOS/zorin-exec-guard) — Execution guard



## BOLT (Binary Optimization and Layout Tool)

[BOLT](https://github.com/llvm/llvm-project/tree/main/bolt) is a post-link binary optimizer from Meta (now part of LLVM). It uses hardware performance counters (perf data) to rearrange the code layout of already-compiled binaries for better instruction cache utilization and branch prediction. Unlike PGO (which requires recompilation), BOLT operates on final binaries.

Potential use: Profile the distro's critical binaries (systemd, GNOME Shell, Mesa, kernel) and optimize their layout. CachyOS uses a similar technique with AutoFDO for the kernel. BOLT can provide 5-15% speedups on hot code paths.

Workflow:
1. Build the binary with relocations preserved (`-Wl,--emit-relocs`)
2. Collect perf data: `perf record -e cycles:u -j any,u -- <binary>`
3. Convert perf data: `perf2bolt -p perf.data -o perf.fdata <binary>`
4. Optimize: `llvm-bolt <binary> -o <binary>.bolt -data=perf.fdata -reorder-blocks=ext-tsp -reorder-functions=hfsort+`

## FEX-Emu (Fast x86 Emulation on AArch64)

[FEX-Emu](https://fex-emu.com/) is a usermode x86 and x86-64 emulator for AArch64 Linux. It allows running x86/x86-64 Linux binaries on ARM64 hardware (e.g., Apple Silicon via Asahi Linux, Qualcomm Snapdragon laptops, Ampere servers).

This is only relevant if the distro targets ARM64 hardware. FEX is comparable to Apple's Rosetta 2 but for Linux. It supports running Steam, Wine/Proton, and many native x86 Linux applications on ARM.

Note: FEX does not emulate x86 on x86 — it is strictly an AArch64-to-x86 translation layer. For x86-on-x86, native execution is used.


# Gaming Mode

## Game Mode THP Settings

Transparent Hugepages (THP) have the kernel allocate memory pages in **2MiB** or 2GiB units instead of 4KiB units as is the platform default on X86. This has been shown to measurably improve gaming performance in many cases. The risk for enabling this is low, as some distros do this by default (such as OpenSUSE). It is also a kernel tunable that can be set at runtime using sysctl.

Proposal: enable THP and disable proactive compaction for gaming sessions, restore to defaults when the session ends (some workloads such as databases can be negatively impacted by memory fragmentation).

Enable when gaming, restore when game ends:
    echo always | sudo tee /sys/kernel/mm/transparent_hugepage/enabled
    echo advise | sudo tee /sys/kernel/mm/transparent_hugepage/shmem_enabled
    echo 0 | sudo tee /proc/sys/vm/compaction_proactiveness
    echo 0 | sudo tee /sys/kernel/mm/transparent_hugepage/khugepaged/defrag

See [Steam Deck Utilities](https://github.com/CryoByte33/steam-deck-utilities/blob/main/docs/tweak-explanation.md)
See [THP Gaming Performance](https://blog.patshead.com/2023/02/enabling-transparent-hugepages-can-provide-huge-gaming-performance-improvements.html)
See [Measuring THP Impact](https://alexandrnikitin.github.io/blog/transparent-hugepages-measuring-the-performance-impact/)