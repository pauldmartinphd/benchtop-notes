# Imported source notes

These are the blocks labeled “From legacy notes” in the initial combined notes. They are retained verbatim for comparison with the edited topic pages. The repository history does not establish the authorship of every passage. Commands, claims, and proposals here retain their original context; this is a source archive, not the current build configuration.

## Applications/Application List.md

````text
---

## From legacy notes: Linux Apps.md

## Web
- Bitwarden
- Linkwarden

## Publications
- Books - Calibre
- PDFs - Okular
- Papers - Zotero

## Education
- Atlas - Marble; Gnome Maps
- Encyclopedia - Kiwix
- Flash Cards - Anki

## Office
- Office - Libreoffice
- Notes - Obsidian

## Broadcasting
Audacity
OBS Studio

## Digital Audio and Video
Kdenlive

## Digital Graphics
Inkscape
Darktable

## CAD:
LibreCAD (2D)
FreeCAD (3D)
OpenSCAD (3D Printing)

### Astronomy
Kstars - Astronomy/Astrophotography
Stellarium - Sky Atlas

### Mathematics
Matlab: Octave
Minitab: JASP
SPSS :PSPP
Wolfram Languae: [Woxi][(https://github.com/ad-si/Woxi)

## Developer
Cyberchef
virt-manager

## Security
Wireshark

# Simple Apps : GTK
- Screenshot/Snip Tool - Printscr
	- Printscr brings up the overlay selection
	- Shift+Printscr takes a screenshot of your entire desktop

# Advanced Apps : QT
- Dolphin
	- Needs text filters
		- Add/Remove Line Numbers...
		- Prefix/Suffix Lines...
		- Sort Lines...
		- Process Duplicate Lines...
		- Process Lines Containing...
		- Remove Blank Lines
		- Canonize...
		- Text Merge...
		- Increase Quote Level
		- Decrease Quote Level
		- Strip Quotes
		- Zap Gremlins...
		- Convert Escape Sequences...
		- Convert Spaces to Tabs...
		- Convert Tabs to Spaces...
		- Strip Trailing Whitespace
		- Normalize Line Endings
		- Normalize Spaces
		- Precompose Unicode
		- Decompose Unicode
	- Needs to be able to reorder, merge and delete PDF pages
	- Need to be able to change font on in-line comments
	- Need to be able to import and attach signature to files
- Gwenview
	- Need to be able to selecte OCRed text in images

### Gaming and Performance
[CPU-X](https://thetumultuousunicornofdarkness.github.io/CPU-X/)
[hardinfo2](https://github.com/hardinfo2/hardinfo2)
[LACT (Linux GPU Configuration Tool)](https://github.com/ilya-zlobintsev/LACT)
[MangoHUD](https://mangohud.com/)

### Security and Technical
[Seer (GDB GUI)](https://github.com/epasveer/seer)

### Developer
[Bustle (D-Bus Visualization)](https://apps.gnome.org/Bustle/)

### KDE Apps
* Dolphin
* Konsole
* Gwenview

### CLI Apps
[Mosh (mobile shell)](https://mosh.org/)

### Unsorted
Thunderbird
GDM Settings
Balena Etcher
KDE Education
Tokodon, AudioTube, PlasmaTube, and Kasts
Impression
Inspector
Fail2ban
Newsflash
Mission Center
RustDesk
RustConn

# Closed Source
LM Studio
Obsidian

# Other
Omnifocus - Planify
Omnigraffle - ??
````

## Applications/Browser Configuration.md

````text
---

## From legacy notes: Brave.md
- Brave is now the default browser. We ship it with a custom policy that disables the following:
    “BraveRewardsDisabled”: true,
    “BraveWalletDisabled”: true,
    “BraveVPNDisabled”: 1,
    “BraveAIChatEnabled”: false,
    “TorDisabled”: true,
    “DnsOverHttpsMode”: “automatic”


---

## From legacy notes: Firefox.md

## Switch browser cache from disk (SSD) to RAM
    browser.cache.disk.enable=false # Change from **true** to **false**
    browser.cache.disk_cache_ssl=false from **true** to **false**
````

## Applications/Terminal and CLI.md

````text
---

## From legacy notes: Terminal Apps.md
Terminal Apps:
    Modern Legacy:
        Shell - Zsh
        Text Editor - neovim
	    Nushell (Structured Data)
	    Helix (Multi-Cursor)
Structured Text:
Markdown
  frogmouth (https://github.com/Textualize/frogmouth)
  ImageMagick
CLI Tools:
  	•	ripgrep (rg) → grep (fast, respects .gitignore)  ￼
	•	fd (fd) → find (simple syntax, fast)  ￼
	•	fzf → fuzzy finder for files/history/branches (glues into everything)  ￼
	•	zoxide → cd + jump-by-frecency (often the biggest QoL upgrade)
	•	eza → ls (maintained fork of exa; exa is effectively dead)  ￼
	•	bat → cat (syntax highlighting, paging)  ￼
	•	delta → git diff pager (syntax-highlighted, readable diffs)  ￼
  1.  Browser - spegel
  2.  Email:
  3.  Calendar
  4.  Todo - taskwarrior
  5.  Notes - frogmouth
  7.  RSS - eilmeldung?
  8.  Password Manager
  9.  Link Manager
Utilities:
  1.  Search
  1.  Word Processor
  2.  Spreadsheets
  2.  Images
Analysis Tools
  1.  Text Editor/IDE - nevoid?
  2.  Debugger
  3.  Hex Editor
  4.  Tshark/termshark
  6.  DevTUI
  7.  KVM/Qemu
  8.  Disassembler/Decompiler
  termshark - https://github.com/gcla/termshark
  1.  Encyclopedia - wik (https://github.com/yashsinghcodes/wik)
  2.  YouTube: https://github.com/Ebrizzzz/Youtube-playlist-to-formatted-text
System Configuration
  1. Bluetooth - https://github.com/pythops/bluetui
  3. Systemd -
Databse:
sqlit - https://github.com/Maxteabag/sqlit
rainfrog - https://github.com/achristmascarl/rainfrog
harlequin - https://github.com/tconbeer/harlequin
Developer:
lazygit - https://github.com/jesseduffield/lazygit
REST - https://github.com/unkn0wn-root/resterm/tree/main
ffdash - https://github.com/bcherb2/ffdash
Youtube-TUI - https://siriusmart.github.io/youtube-tui/
````

## Networking/Network Services.md

````text
---

## From legacy notes: Network Services.md

# Security
Inbound Firewall: ufw
Outbound Firewall: OpenSnitch

## Content and Media
File Sharing: SSHFS
Screen Sharing: RustDesk

## Advanced
Remote Management: Cockpit
Remote Login: Web
Bitwarden
Tailscale

### Content and Media
File Sharing
Media Sharing
Screen Sharing
Content Caching

### Accessories and Internet
Bluethooth Sharing
Printer Sharing
Web Sharing

### Advanced
Remote Management
Remote Login
Remote Application Scripting

### Other
Target Disk Mode

### Deprecated:
Airplay Receiver
Xgrid Sharing
Web Sharing
DVD or CD Sharing
````

## Networking/Printing.md

````text
---

## From legacy notes: Linux Printing (IPP Only).md
	•	Transport: IPP over HTTP
	•	Formats: PDF or Apple Raster
	•	Discovery: mDNS / Bonjour
Mopria is an industry consortium that standardized driverless IPP printing across vendors. It is effectively:
	•	IPP Everywhere + Mopria job-ticket profiles
	•	PDF / PCLm / JPEG raster
	•	mDNS or WSD discovery
	1.	V4 Print Driver Model
Modern Windows avoids vendor PCL/PS drivers and instead relies on class drivers.
	2.	Microsoft IPP Class Driver
This is the default for all network and USB network-function printers.
It conforms to:
	•	IPP Everywhere
	•	WSD/WS-Print (for discovery only; job transport increasingly IPP)
	3.	Windows supports IPP over USB, the same profile used on ChromeOS, iOS, and Linux.
What your distribution actually needs
If you provide:
	•	CUPS with full IPP Everywhere support
	•	mDNS/Bonjour discovery (Avahi)
	•	PDF and PWG/Apple Raster filters
	•	IPP-over-USB (ipp-usb)
…then you support:
	•	AirPrint
	•	Windows Modern Print (IPP Class Driver)
	•	ChromeOS
	•	Android
	•	All current enterprise MFPs that implement IPP Everywhere
No proprietary drivers are required unless a user insists on vendor-specific finishing or accounting extensions.
Here is the complete, minimal set for a modern driverless stack on openSUSE
Core printing: CUPS with IPP Everywhere
Install:
cups-filters
cups-filters-ipp
cups-filters-ghostscript
Discovery: AirPrint / Mopria
Install:
avahi-utils
Avahi provides Bonjour/mDNS service advertisements and discovery. AirPrint and Mopria depend on this.
IPP over USB (critical for modern printers)
Install:
This replaces usbbackend with a proper IPP service over a localhost port. All modern USB printers use this.
Packages you do NOT need
If your distro only supports IPP Everywhere:
	•	No HPLIP
	•	No Epson ESC/P-R
	•	No Canon UFR2
	•	No Brother LPR
	•	No foomatic-db
	•	No PPD packs
	•	No proprietary filters
````

## Networking/Self-Hosted Services.md

````text
---

## From legacy notes: Open Source Protocols and Servers.md
Tailscale and Headscale (VPN)
RustDesk (Remote Desktop)
rclone (Cloud Storage)
Sunshine and Moonlight (Game Streaming)
Bitwarden and Vaultwarden (Password Manager)
LinkWarden (Link Manager)
Floccus (Bookmark Manager)
Brave Browser Sync (Browser Sync)
Syncthing (File Synchronization, Cloud Storage w/ Server)
CAST (Chromecast/Airplay)
LocalSend (AirDrop)
SSH/Mosh
- NextCloud (Dropbox/iCloud)
- Wireguard
- OpenVPN
- AirPlay
- Firefox Sync
````

## OpenSUSE/OpenSUSE Configuration.md

````text
---

## From legacy notes: OBS Custom Repository.md
OpenSUSE Kernel:
	NVIDIA Module
	Binder and ASHMEM Modules
	Zfs Module
	1000hz Tick Rate
	system76-scheduler
	adw-gtk3
	pipewire-nonfree-codecs
	dislocker
Flatpak:
	Waydroid:
		https://gist.github.com/Saren-Arterius/c5bc39199552a5c244449b0ce467d6b6
		https://bugzilla.opensuse.org/show_bug.cgi?id=1189456
		https://linux32bituefi.blogspot.com/2021/12/install-waydroid-in-opensuse-tumbleweed.html
	    https://github.com/SGNight/Arm-NativeBridge
	Cyberchef
	SD Memory Card Formatter for Linux
	Nautilus w/ Sushi
	Gnome Software


---

## From legacy notes: OpenSUSE Configuration.md

# Weaknesses
- Disk Partitioning
- Cryptography
- Remote Management
- Automatic Disk Unlock

# Core Components
OpenRGB-udev-rules
rasdaemon

##### Pipewire
 TODO: non-free Codecs:
[Link](https://github.com/mikeroyal/PipeWire-Guide)

## Enable Avahi
    sudo systemctl status avahi-daemon

## Hostname
/etc/nsswitch.conf.d/10-hostname.conf
Change line hosts:  files mdns_minimal [NOTFOUND=return] dns to read:

# Security
OpenSUSE by default disallows wheel sudo; also sets Defaults targetpw.  Need to change both settings and then lock root

### polkit
/polkit-1/rules.d/50-wheel-auth-self.rules

### Performance Monitoring
	Requires:       htop
	Requires:       iotop-c
	Requires:       nvtop
	Requires:       iftop
	Requires:       nethogs
	Requires:       ss
	Requires:       powertop
	Requires:       atop

# ToDo
  * Change to sudo
  * Command Line Interface
````

## Performance/Benchmarking.md

````text
---

## From legacy notes: Benchmarking.md

# Latency
Measure GUI FPS Under
* Large file copies
* Video encoding script
* All core compile
````

## Reference/Research Links.md

````text
---

## From legacy notes: Manuals and Documentation.md
GNU (https://www.gnu.org/)
Kernel (https://www.kernel.org/)
SystemD (https://systemd.io/)
NetworkManager (https://www.networkmanager.dev/)
BlueZ (https://www.bluez.org/)
Tuned (https://tuned-project.org/)
Pipewire (https://www.pipewire.org/)
Mesa (https://mesa3d.org/)
Freedesktop (https://www.freedesktop.org/)
````

## Scratch.md

````text
---

## From legacy notes: Scratch.md

### App Installation
https://github.com/linuxmint/webapp-manager
https://www.appimagehub.com/
https://www.appimagehub.com/p/1228228
https://github.com/prateekmedia/appimagepool

### Fonts
https://news.ycombinator.com/item?id=30705078
https://github.com/pdeljanov/infinality-remix/issues/13
https://github.com/pdeljanov/infinality-remix
https://gist.github.com/cryzed/e002e7057435f02cc7894b9e748c5671
https://wiki.archlinux.org/title/Font_configuration

##### System
https://wiki.archlinux.org/title/Improving_performance
https://wiki.archlinux.org/title/Gaming#Improving_performance
https://wiki.archlinux.org/title/sysctl
https://wiki.archlinux.org/index.php/Hardware_video_acceleration
https://www.clearlinux.org/clear-linux-documentation/guides/index.html
https://www.clearlinux.org/clear-linux-documentation/guides/clear/performance.html

##### Kernel
https://liquorix.net/#features
https://github.com/zen-kernel/zen-kernel/wiki/Detailed-Feature-List
https://github.com/clearlinux-pkgs/linux/
https://xanmod.org/
https://news.ycombinator.com/item?id=46366998

##### Distro Defaults
https://github.com/pop-os/default-settings/
https://github.com/CachyOS/CachyOS-Settings

##### Applications
https://github.com/FeralInteractive/gamemode/
https://github.com/pop-os/system76-scheduler
https://wiki.archlinux.org/title/Preload
https://handwiki.org/wiki/Prelink
https://github.com/Nefelim4ag/Ananicy
https://github.com/hakavlad/nohang
https://github.com/AdnanHodzic/auto-cpufreq
https://github.com/oracle/bpftune
https://github.com/ZorinOS/zorin-exec-guard

##### Distro Defaults
https://github.com/clearlinux/clr-power-tweaks

##### Power Profiles Daemon
https://github.com/pop-os/system76-power
https://tuned-project.org/
https://linrunner.de/tlp/
https://gitlab.freedesktop.org/upower/power-profiles-daemon

##### Applications
https://www.smartmontools.org/
https://github.com/intel/thermal_daemon
https://wiki.archlinux.org/title/Hdparm
https://sg.danny.cz/sg/sdparm.html

### Security
https://kspp.github.io/
https://www.kicksecure.com/wiki/Security-misc
https://github.com/Kicksecure/security-misc
https://www.clearlinux.org/clear-linux-documentation/guides/clear/security.html
https://github.com/evilsocket/opensnitch

##### Cryptography
https://github.com/canonical/crypto-config
https://gitlab.com/redhat-crypto/fedora-crypto-policies
https://en.opensuse.org/SDB:Crypto-policies
Idea: fTPM Integration, YubiKey, NitroKey Integration

### Rust
https://discourse.ubuntu.com/t/carefully-but-purposefully-oxidising-ubuntu/56995
https://www.phoronix.com/news/Ubuntu-25.10-sudo-rs-Default
https://ubuntu.com/blog/tpm-backed-full-disk-encryption-is-coming-to-ubuntu

### Kernel Documentation
https://www.kernel.org/doc/html/latest
https://lwn.net/Kernel/Index/
https://kernelnewbies.org/
https://wiki.archlinux.org/title/Kernel_parameters

### Hardware Specific Tools
https://openrgb.org/
https://openrazer.github.io/
https://github.com/linux-surface
https://asus-linux.org/
https://docs.mrchromebox.tech/
https://asahilinux.org/
https://t2linux.org/

### Accessibility
http://fireborn.mataroa.blog/blog/i-want-to-love-linux-it-doesnt-love-me-back-post-1-built-for-control-but-not-for-people/

##### Tailscale
https://news.ycombinator.com/item?id=46531925
https://github.com/tailscale/tailscale/issues/17654
https://github.com/tailscale/tailscale/issues/18288
https://github.com/tailscale/tailscale/issues/18302

##### Aeon
https://www.reddit.com/r/AeonDesktop/comments/1pwuvnw/pcr15_validation_again_unable_to_reenroll_please/
https://www.reddit.com/r/AeonDesktop/comments/1o9wip0/the_validation_of_pcr_15_failed/

### Partitioning Apps
KDE Partition Manager

### Supported Models
Laptops:
  Apple MacBook
  Microsoft Surfcace
  ASUS ROG/ProARt
  Razer Blade
  Lenovo ThinkPad
  Dell Precision/Latitude/XPS
  HP Elitebook
  HP Zbook
  
### CachyOS Optimizations
CachyOS Kernel
    Uses the BORE scheduler.
    Built with clang and ThinLTO
    Profiled with our own AutoFDO Profile
        Script used to profile the kernel.
   •	Choose between 3 kernel schedulers and various sched-ext schedulers for improved responsiveness
	•	AMD P-State Improvements
	•	Latest BBRv3 by Google
	•	le9uo for significantly improved responsiveness during high memory load
	•	Up-to-date NTSYNC patchset, used with a compatible build of wine/proton
	•	Compatibility with T2 MacOS devices with patches from t2linux
	•	Allows reading per-core CPU energy usage for AMD users
	•	ACS Override and v412loopback
	•	VHBA module for emulating CD/DVD-ROM devices
	•	Latest ZSTD patchset
	•	Various other patches that focus on improving performance (optimized compiler flags, cryptographic improvements, memory management tweaks)
	•	x86-64-v3: 5%-20% performance uplift compared to x86-64.
	•	x86-64-v4: Delivers substantial performance gains through AVX512 support, depending on the workload.
	•	Zen 4/5: In addition to the x86-64-v4 instruction set, the following are added:

##### Transparent Hugepages
I propose we enable THP and disable proactive compaction for gaming sessions and set these back to default when the session ends (as some workloads such as databases can be negatively impacted by memory fragmentation that this can cause).
My proposal is to enable the following when gaming and restore when game ends:
See e.g. [https://github.com/CryoByte33/steam-deck-utilities/blob/main/docs/tweak-explanation.md](https://github.com/CryoByte33/steam-deck-utilities/blob/main/docs/tweak-explanation.md)
See also [https://blog.patshead.com/2023/02/enabling-transparent-hugepages-can-provide-huge-gaming-performance-improvements.html](https://blog.patshead.com/2023/02/enabling-transparent-hugepages-can-provide-huge-gaming-performance-improvements.html)
See also [https://alexandrnikitin.github.io/blog/transparent-hugepages-measuring-the-performance-impact/](https://alexandrnikitin.github.io/blog/transparent-hugepages-measuring-the-performance-impact/)

##### Tick Rate
CONFIG_HZ=1000 last but not least, the only option that is *only* tunable at compile time. As already mentioned there is a potential risk of regressions for CPU-intensive applications, but they can be mitigated (and maybe they could even outperformed) with NO_HZ_FULL. On the other hand, HZ=1000 can improve system responsiveness, that means most of the desktop and server applications will benefit from this (the largest part of the server workloads is I/O bound, more than CPU-bound, so they can benefit from having a kernel that can react faster at switching tasks), not to mention the benefit for the typical end users applications (gaming, live conferencing, multimedia, etc.).
USB Disks
  1.  Synchronous writes on slow disks (USB Flash drives)
  2. TRIM over USB for fast disks
GNOME Settings
    https://github.com/pop-os/firmware-manager
    https://www.reddit.com/r/gnome/comments/qyi9lc/does_gnome_plans_to_integrate_firewall_settings/
Disable tmp on tmpfs
ZRAM Hibernate
  Linux Resume:
    Reset Bluetooth
    Reset WiFi
    Reset Trackpad
    Reset Touchscreen
CryptSetup Opal
Facebook BOLT
Optimal Encryption Sector Size (Fedora 35)
Filesystems:
Linux patching research
  Theory: rolling release patches security bugs faster than forked LTS
  Theory: pip/npm better than distro-managed libraries
https://github.com/vinceliuice/MacTahoe-gtk-theme
https://news.ycombinator.com/item?id=46031208
https://github.com/somepaulo/MoreWaita
Enable 2MB THP by Default
https://www.phoronix.com/news/Glibc-malloc-2MB-THP-AArch64
Libreoffice writer did not respect dark mode change and icons do not show up
Browser Cache
**Realtime**
Group Limits
User pmartin is currently not member of a group that has sufficient rtprio (0) and memlock (-1) set. Add yourself to a group with sufficent limits set, i.e. audio or realtime, with 'sudo usermod -a -G <group_name> pmartin. See also https://wiki.linuxaudio.org/wiki/system_configuration#audio_group
RT Priorities
Could not assign a 80 rtprio SCHED_FIFO value due to the following error: [Errno 1] Operation not permitted. Set up limits.conf. See also https://wiki.linuxaudio.org/wiki/system_configuration#limitsconfaudioconf
Power Management
Power management can't be controlled from user space, the device node /dev/cpu_dma_latency can't be accessed by your user. This prohibits DAWs like Ardour and Reaper to set CPU DMA latency which could help prevent xruns. For enabling access see https://wiki.linuxaudio.org/wiki/system_configuration#quality_of_service_interface
Swappiness
vm.swappiness is set to 180 which is too high. Set swappiness to a lower value by adding 'vm.swappiness=10' to /etc/sysctl.conf and run 'sysctl --system'. See also https://wiki.linuxaudio.org/wiki/system_configuration#sysctlconf

## Modern Linux:
	Everything is really a file
	Text format for all personal data; greppable
	Tag-based FS Tags Cross Platform into Virtual Folders
	    Implement Tags using hard link so a vnode with two links is given two “tags” in Dolphin
	    Look into ZFS Hard Link and Tag Support
	ZFS Root Distributed with Low Latency Kernel
	Subvolume for /home or /home on Separate Array
	No Support for distributed /
	Fix Linux Kernel in ESP
	Toggle for “Cross-platform” or “Next Generation” support for /home
		Cross-platform
			No hard links
			Case insensitive FS
			Limited filename character set
			Full POSIX
		Single Platform
			Tags implemented through hard links
			Case sensitive FS
			Full filename character set
			Ignore POSIX
	Do we need all file metadata attributes?  Can we simply record last file modification time (or creation time if not modified?)
````

## Security/Security Tools.md

````text
---

## From legacy notes: Open Source Security Tools.md
﻿Security Tools:
	Exploit Scanning
	Web Security Scanning
	MITM Proxying
	Memory Dump Analyzer w/ Entropy Scanner
	Disk Forensics Tools
	OS Hash-check Installs


---

## From legacy notes: Security Tools.md

# Security Tools
- Wireshark
- Cyberchef
- [devtui](https://github.com/skatkov/devtui)
- Mitmproxy
- L0phtcrack
- Sleuthkit
- Autopsy
- Volatility
- Gdb (See if GUI Tool)
- KVM/QEMU
````

## System Core/Distro Vision.md

````text
---

## From legacy notes: Immutable Distro Vision.md

# Subsystems
* Windows

# Security
  * Rolling Release Patches
  * Userspace-only Support for

# Filesystems:
Base Filesystem COW w/ Snapshots
	bcachefs

# Pre-Packaged Environment
Configure Compression and Filesystem Format Support
    1.  Compression
        sudo dnf install cabextract lha arj lzip unrar pax p7zip p7zip-plugins p7zip-doc sharutils unzix unace xar xdms xz
    2.  Filesystems
        sudo dnf install dmg2img simg2img fuse-exfat exfat-utils squashfuse squashfs-tools zfs-fuse fuse-afp fuse9p squashfuse orangefs-fuse fuse-sshfs fuse-dislocker fuse-encfs
          NTFS (FUSE)
          EXFAT (FUSE
          FAT32 (FUSE)
          HFS+ (FUSE)
          APFS (FUSE https://github.com/linux-apfs)
          Android Adoptable Storage (https://nelenkov.blogspot.com/2015/06/decrypting-android-m-adopted-storage.html)
          Samsung Encrypted SD Card ?
          BitLocker ?
          FileVault ?
    3.  yq: command-line YAML, JSON, XML, CSV and properties processor
          https://github.com/mikefarah/yq
    4.  pandoc: command-line document conversion format
    5.  Video Codecs
    6.  Image Formats

# Fonts
Infinality Font Rendering
ClearType Fonts
Microsoft TTF Support (and default for OpenOffice)

# Modernized UNIX Protocols?
  Bonjour Service Dsicovery: Avahi
  Syncthing (In-Network Data Exchange)
  Cryptomator Cloud Encryption
  LUKS Volume Encryption
  Nextcloud
  Localsend
  SMB3 File Sharing (Considering whether to modify for lowest common denominator or highest)
	*	Driverless AirPrint/IPP/WSD Printing/Scanning (CUPS/SANE)
	*	RDP low latency replacement - moonlight?
	*	ZFS: https://www.poolsman.com/

# Audio Cues
  Any delayed response/action
  Drag and drop/file copy
  File download
  Empty trash
  Action not allowed
    E.g. click outside box when input required
  https://utcc.utoronto.ca/~cks/space/blog/linux/SystemSoundsShouldBeGranular

# Drivers
Complete Driver Packaging and Firmware Built-In
	Printers, Scanners, GPU, WiFi, Function Keys
	Proprietary Drivers built-in
	Proprietary Firmware built-in
	Optimus/Dynamic GPU Support


---

## From legacy notes: Linux Distro Ideas.md
Distro Configured Uses:
	Machine Learning
	Data Science
	Virtualization
	  GUI: Virt-Manager; Boxes
	  Web (Incus)
	Software Development
	  Kubernetes
	  GUI: Podman Desktop
	System Administration
	  Distrobox/Distrosheff
	Audio and Multimedia
	  Flatpak (Consider)
	    Bazaar Application Store
	    Warehouse for Flatpak management
	    Flatseal
		Consider as Per-user application environment; instead of distrobox
		    “Bluefin specifically ships upstream tools in lieue of custom applications. The idea of a "distribution app store" has proven to be unsustainable for desktop application authors, so Bluefin ships tools like Bazaar and Homebrew instead. Additionally the team purposely ensures that the workflows used in Bluefin remain not only distribution agnostic, but operating system agnostic. For example, podman, docker, and flatpak instead of distribution specific tooling, etc.”
Tailscale Integrate with NetworkManager
rclone - mount nearly any remote storage service onto your local machine, great for multi-machine setups
restic - A modern backup program for your files
** Quality of Life Features **
Starship terminal prompt enabled by default
Solaar - included for managing Logitech mice along with libratbagd
Extra udev rules for game controllers and other devices included out of the box
https://docs.projectbluefin.io/introduction
https://docs.projectbluefin.io/bluefin-dx
https://docs.projectbluefin.io/command-line
Modern Filesystem Hierarchy
````

## System Core/Power Management.md

````text
---

## From legacy notes: Battery and Power Management.md
powertop2tuned and tuned profile config
Zypper Enable Remove Orphans
````

## UX and Desktop/Fonts.md

````text
---

## From legacy notes: Font Rendering.md
1. Create the following symlinks using root to instruct freetype2 to use good-looking rendering defaults:
2. Modify (or create) `/etc/fonts/local.conf`
		<?xml version="1.0"?>
		<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
		<!-- /etc/fonts/local.conf file for local customizations -->
		<fontconfig>
		  <!-- Replacements from http://bohoomil.com/doc/05-fonts/ (until ibfonts-meta-extended) -->
		    <family>serif</family>
		    <prefer><family>Heuristica</family></prefer>
		  </alias>
		    <family>sans-serif</family>
		      <prefer>
		        <family>Noto Sans</family>
		        <family>Noto Sans CJK SC</family>
		      </prefer>
		  </alias>
		    <family>monospace</family>
		    <prefer>
		      <family>Liberation Mono</family>
		      <family>Noto Sans Mono CJK SC</family>
		    </prefer>
		  </alias>
		    <family>fantasy</family>
		    <prefer><family>Signika</family></prefer>
		  </alias>
		    <family>cursive</family>
		    <prefer><family>TeX Gyre Chorus</family></prefer>
		  </alias>
		    <test name="family"><string>Arial</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Liberation Sans</string>
		  </match>
		    <test name="family"><string>Arial Narrow</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Liberation Sans Narrow</string>
		  </match>
		    <test name="family"><string>Book Antiqua</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>TeX Gyre Bonum</string>
		  </match>
		    <test name="family"><string>Calibri</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Carlito</string>
		  </match>
		    <test name="family"><string>Cambria</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Caladea</string>
		  </match>
		    <test name="family"><string>New Century Schoolbook</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>TeX Gyre Schola</string>
		  </match>
		    <test name="family"><string>Comic Sans MS</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Signika</string>
		  </match>
		    <test name="family"><string>Consolas</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Droid Sans Mono Slashed</string>
		  </match>
		    <test name="family"><string>Constantia</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Merriweather</string>
		  </match>
		    <test name="family"><string>Corberl</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Merriweather Sans</string>
		  </match>
		    <test name="family"><string>Courier New</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Courier Prime</string>
		  </match>
		    <test name="family"><string>Geneva</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Noto Sans</string>
		  </match>
		    <test name="family"><string>Georgia</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Gelasio</string>
		  </match>
		    <test name="family"><string>Helvetica</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Liberation Sans</string>
		  </match>
		    <test name="family"><string>Helvetica Narrow</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Liberation Sans Narrow</string>
		  </match>
		    <test name="family"><string>Helvetica Neue</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Open Sans</string>
		  </match>
		    <test name="family"><string>Impact</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Oswald</string>
		  </match>
		    <test name="family"><string>ITC Zapf Chancery</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>TeX Gyre Chorus</string>
		  </match>
		    <test name="family"><string>Lucida Calligraphy</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Quintessential</string>
		  </match>
		    <test name="family"><string>Lucida Handwriting</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Quintessential</string>
		  </match>
		    <test name="family"><string>Lucida Casual</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>CantoraOne</string>
		  </match>
		    <test name="family"><string>Lucida Console</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Droid Sans Mono</string>
		  </match>
		    <test name="family"><string>Lucida Sans Typewriter</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Liberation Sans Mono</string>
		  </match>
		    <test name="family"><string>Lucida Fax</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Luxi Mono</string>
		  </match>
		    <test name="family"><string>Lucida Sans</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Droid Sans</string>
		  </match>
		    <test name="family"><string>Lucida Grande</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Droid Sans</string>
		  </match>
		    <test name="family"><string>Palatino Linotype</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>TeX Gyre Pagella</string>
		  </match>
		    <test name="family"><string>SegoeUI</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>WeblySleek UI</string>
		  </match>
		    <test name="family"><string>Symbol</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Symbola</string>
		  </match>
		    <test name="family"><string>Tahoma</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>DejaVu Sans Condensed</string>
		  </match>
		    <test name="family"><string>Times New Roman</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Liberation Serif</string>
		  </match>
		    <test name="family"><string>Trebuchet MS</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Ubuntu</string>
		  </match>
		    <test name="family"><string>Verdana</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>DejaVu Sans</string>
		  </match>
		    <test name="family"><string>Wingdings</string></test>
		    <edit name="family" mode="assign" binding="strong">
		      <string>Symbola</string>
		  </match>
		</fontconfig>
3. Install Distro Fonts
4. Google Fonts:
- Caladea (`ttf-caladea`)
- Carlito (`ttf-carlito`)
- DejaVu (`ttf-dejavu`)
- Impallari Cantora (`aur/ttf-impallari-cantora`)
- Liberation (`ttf-liberation`)
- Noto (`noto-fonts`)
- Open Sans (`ttf-opensans`)
- Overpass (`otf-overpass`)
- Roboto (`ttf-roboto`)
- TeX Gyre (`tex-gyre-fonts`)
- Ubuntu (`ttf-ubuntu-font-family`)
- Courier Prime (`aur/ttf-courier-prime`)
- Gelasio (`aur/ttf-gelasio-ib`)
- Merriweather (`aur/ttf-merriweather`)
- Source Sans Pro (`aur/ttf-source-sans-pro-ibx`)
- Signika (`aur/ttf-signika`)
2. [Install Envision Settings](https://www.reddit.com/r/linux/comments/1bh1x80/tweaks_for_the_freetype_font_rendering/) [Github](https://github.com/maximilionus/freetype-envision)


---

## From legacy notes: Open Fonts.md
Atkinson Hyperlegible
GNU Unifont
Google Noto
Intel’s One Mono
JetBrains Mono
Microsoft Cascadia Code
NebulaSans
````

## UX and Desktop/GNOME Configuration.md

````text
---

## From legacy notes: GNOME Configuration.md

## Out of Memory User Dialog
[https://gitlab.gnome.org/Teams/Design/whiteboards/-/issues/340](https://gitlab.gnome.org/Teams/Design/whiteboards/-/issues/340)

## Notifications
Apps Should Dismiss Outdated Notifications

## Search
* Gnome Fuzzy App Search (Possible Integrated into the Shell in the Future: https://gitlab.gnome.org/GNOME/glib/-/issues/1152)

## Drag and Drop
Drag Files to dock
Drag window while changing desktops
Drag icons to sidebar
Drag text/images to desktop
Cannot Drag Icon from background window without raising the window as a result
	https://gitlab.gnome.org/Teams/Design/whiteboards/-/issues/255

#### Cloud Sync
https://gitlab.gnome.org/Teams/Design/whiteboards/-/issues/335
https://discourse.gnome.org/t/proposal-integrate-syncthing-into-gnome-settings/15387
Dotfiles
Flatpak Apps
Gnome Shell Extensions
Gnome Shell Configuration

#### Other
Color Picker: Standalone App + QT + GTK
Global Option to open all files in tabs in QT + GTK Applications
Default Templates in Template Folder

##  GDM
- GDM login screen on wrong display
	- https://gitlab.gnome.org/GNOME/gnome-shell/-/issues/3867
	- https://github.com/thiggy01/change-gdm-background/issues/15

## Endeavor
- Nested Tasks
	- https://gitlab.gnome.org/World/Endeavour/-/issues/488

## GNOME Initial Setup
- GNOME Initial Setup - Wrong WiFi password cannot be re-entered

## Nautilus
When moving a directory containing a file that the user does not have permissions to access, half of the directory gets moved before the error, leading to an inconsistent state.  Instead, moves should first succeed 100% before any files are deleted
When copying or moving files, copy stops on first error.  Instead, copy should continue while error dialog is displayed.

## Shell
When an application inhibits sleep or reboot there should be a notification

## Theming
* Adwaita
    https://github.com/eylles/adw-gtk2-colorizer
    https://github.com/lassekongo83/adw-gtk3
    https://github.com/dp0sk/adw-gimp3
	https://github.com/RichardSepsi/adw-inkscape
	https://github.com/nukusaba/Libadwaita-KDE/
	https://github.com/GabePoel/KvLibadwaita
	https://github.com/rafaelmardojai/firefox-gnome-theme
	https://github.com/rafaelmardojai/thunderbird-gnome-theme
	https://github.com/tkashkin/Adwaita-for-Steam
	https://github.com/piousdeer/vscode-adwaita
	https://github.com/ricewind012/discord-gnome-theme
	https://github.com/birneee/obsidian-adwaita-theme
* Yaru (https://github.com/ubuntu/yaru)
	Solves: Can't Distinguish active from Inactive Window
	Black Headerbar on Active Window; White on Inactive

# Gnome Settings
Configuration Settings (User May Change, needs gnome)
- Hostname
- Sync(thing)
- Firewall
System Settings: (User shouldn’t change)
- Bootloader
- NetworkManager
- SystemD

## Blur My Shell
  https://github.com/aunetx/blur-my-shell/issues/455
  https://github.com/aunetx/blur-my-shell/issues/757

## Coverflow Alt-tab
  https://github.com/dsheeler/CoverflowAltTab/issues/13

## Dash to Dock
Gnome Dock Launch Feedback
  https://github.com/micheleg/dash-to-dock/issues/49
    - https://github.com/home-sweet-gnome/dash-to-panel/issues/2218
  https://github.com/micheleg/dash-to-dock/pull/574
  https://github.com/micheleg/dash-to-dock/issues/1029

## GTK4 Desktop Icons Next Generation (DING)
Include but toggle

## Just Perfection
  Click to Close Overview (Repalce click-to-close-overview@l3nn4rt.github.io)
  Restore Desktop Thumbnails (Replace GNOME 4X UI Improvements)

## Rounded Window Corners Reborn
Unround the bottom corners (Not currently possible)
Corner radius of 15 for consistency between GTK3 and libadwaita
https://github.com/flexagoon/rounded-window-corners/issues/36
https://gitlab.gnome.org/GNOME/gnome-shell/-/issues/7903
https://github.com/flexagoon/rounded-window-corners/issues/43

## Search Light
- Consider
- Integrate with Blur My Shell

## Tiling Shell
- Switch desktop while dragging and hovering on screen edge
- Switch desktops with keyboard while dragging

## Transparent Window Moving
- Switch desktop while dragging and hovering on screen edge
- Switch desktops with keyboard while dragging

## Weather o'Clock
Consider:
Caffeine (caffeine@patapon.info)
Clipboard Indicator (clipboard-indicator@tudmotu.com)
AlphabeticalAppGrid@stuarthayhurst
Always-Show-Titles-In-Overview
applications-overview-tooltip@RaphaelRochet
* Gnome Fuzzy App Search (Possible Integrated into the Shell in the Future: https://gitlab.gnome.org/GNOME/glib/-/issues/1152)
https://extensions.gnome.org/extension/8226/maximize-to-empty-workspace-2025/
Wifi QR Code
Bangs Search
````

## UX and Desktop/GNOME Tablet Mode.md

````text
---

## From legacy notes: Gnome Tablet Interface.md
Gnome Tablet Mode
  Keyboard like iPad
  Increase menu bar size
  Automatic Maximize to new desktop
  Bigger Close Button
  Remove Minimize and Maximize button
  Remove Drag to Maximize
  Button to Disable
Use These GNOME Extensions To Make An iPad Like GNOME Desktop:
\-[Maximize To Empty Workspace](https://extensions.gnome.org/extension/3100/maximize-to-empty-workspace/): This extension moves windows when they're maximized automatically to an empty workspace so every window has its workspace
\-[Auto Activities](https://extensions.gnome.org/extension/5500/auto-activities/): This extension automatically opens the Activities view when there are no windows (I changed it to the App Grid)
\-[Always Show Titles in Overview](https://extensions.gnome.org/extension/1689/always-show-titles-in-overview/): This extension makes titles of apps appear even if you aren't hovering over the window (I also enabled the option always to show the close button)
\-[Improved OSK](https://github.com/nick-shmyrev/improved-osk-gnome-ext): This extension adds extra keys to the onscreen keyboard, and a button in the panel and you can make it bigger or smaller (depending on your screen size and scaling factor, the normal OSK might be very small). It also fixes some annoying bugs
\-[Custom Hot Corners - Extended](https://extensions.gnome.org/extension/4167/custom-hot-corners-extended/): I had to enable the option, Use fallback hot corner triggers" and created the following hot corners: Top left (Toggle Overview - App Grid), Bottom left (Previous workspace), and Bottom right (Next workspace). These gestures work by swiping from these screen corners to the rest of the screen.
````

## UX and Desktop/Input Devices.md

````text
---

## From legacy notes: Touchpad.md
It isn't... You can see this in an open source JavaScript implementation of kinetic scrolling by Apple called PastryKit[3] using a magic number momentum * 0.9.
The problem is, that on modern Linux environments, there is no clear responsibility for where scroll handling code belongs. Especially Kinetic / Inertial scrolling is handled way different than in macOS.
There is libinput (for handling and redirecting input events)
There is the display server
There is the compositor
There is the window manager
There is the app layer (every App, like Firefox, Gimp,
Currently kinetic scrolling is implemented on the App layer, every app has to handle the scrolling events manually to provide kinetic scrolling. This is not the case in macOS... the kinetic scrolling / rubber banding is handled within the OS.
In my opinion, the scrolling code could belong into the compositor, so that not every app developer has to write code to handle the scrolling, but still prevent unwanted effects like kinetic scrolling transfer between windows. Additionally, the kinetic scrolling approach is not configurable in Gnome... some touchpads / screens are scrolling way to fast, some are too slow...
https://news.ycombinator.com/item?id=39607747
After many hours of dissecting the algorithm, we concluded that Apple is in fact using magic numbers. And the magic number is: (drumroll) momentum * 0.95.
Basically, while the touch lasts, apple lets you move the screen 1:1.
On touch end Apple would get momentum by dividing number of pixels that the user had swiped, and time that the user has swiped for. If the number of pixels was less than 10 or time was less than 0.5, momentum would be clamped to zero.
Anyways, once the momentum (speed) was known to us, they would multiply it by 0.95 in every frame, and then move the screen by that much.
So idiotically simple and elegant, that it hurts. :)
https://stackoverflow.com/questions/38619717/need-help-dissecting-and-recreating-the-perfect-scroll-easing-based-on-pastrykit
I am certain that i am not the only person ever to feel amused by the fact that in 2017, in the era of UX, not every scroll is the same. On second thought, it may be a poor decision to standardize everything, and while you may argue that one type of scroll physics is better than other, this is in fact a question of opinion. And my boss’ opinion was that we need to implement a clone of iOS scroll physics into our Unity mobile app.
https://medium.com/homullus/recreating-native-ios-scroll-and-momentum-2906d0d711ad


---

## From legacy notes: Universal Keyboard Shortcuts.md

### Idea: Modal Keys
Window key for Window Management
    Window key launch overview
    Window-tab to switch between windows
    Window-left/right for tiling
    Window-up/down for minimize/maximize
Alt key for Evironment management (Manage all apps)
    alt key open app view
    alt-tab switch between applications
Ctrl key for Running Application (Control running/focused app)
	ctrl-tab switch between application tabs
Caps key for controlling terminal

## Keyboard Shortcuts
Middle Click -> Minimize
Double Click -> Maximize

### CLI Interface UI Paradigms
  Space Shows Command Palatte (On desktop for GUI or in modal-CLI apps)
  Mode Displayed on Screen
````
