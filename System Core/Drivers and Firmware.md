# Drivers and Firmware

The lists below describe the intended hardware and format coverage. Package commands are working references and still need to resolve against the image’s selected repositories.

## Goal
Complete driver packaging and firmware built-in:

* Printers, Scanners, GPU, WiFi, Function Keys
* Proprietary drivers built-in
* Proprietary firmware built-in
* Optimus/Dynamic GPU support

## Video Codecs

Ensure hardware-accelerated decoding (VA-API / VDPAU) and all common software codecs are pre-installed.

### Hardware Acceleration

    # Intel (recent):
    sudo zypper install intel-media-driver     # iHD driver (Broadwell+)
    # Intel (legacy):
    sudo zypper install libva-intel-driver     # i965 driver (Sandy Bridge–Coffee Lake)
    # AMD (built into Mesa):
    # No additional packages needed; Mesa's radeonsi/RADV handle VA-API natively
    # NVIDIA:
    # NVDEC/NVENC provided by the proprietary driver

### Software Codecs (from Packman repo)

    sudo zypper install ffmpeg gstreamer-plugins-bad gstreamer-plugins-ugly gstreamer-plugins-libav
    sudo zypper install libavcodec-full        # All ffmpeg codecs including non-free (h264, h265, AAC)
    sudo zypper install x264 x265 libvpx libdav1d

Key codec coverage:

* **H.264/AVC** — Universal web video, Blu-ray (x264 encoder, openh264 decoder)
* **H.265/HEVC** — 4K streaming, modern cameras (x265 encoder)
* **VP9** — YouTube, WebRTC (libvpx)
* **AV1** — Open video codec; YouTube, Netflix (dav1d decoder, SVT-AV1 or rav1e encoder)
* **AAC** — Standard audio codec (fdkaac for high quality, or ffmpeg's built-in)
* **FLAC, Vorbis, Opus** — Open audio codecs (included in base gstreamer)
* **AC3/DTS** — Surround sound for movies (a52dec, libdca)

### Verification

    vainfo                    # Check VA-API support
    vdpauinfo                 # Check VDPAU support (NVIDIA)
    gst-inspect-1.0 | grep -i "264\|265\|av1\|vp9"   # Check GStreamer codec availability

## Image Formats

    sudo zypper install libjpeg-turbo libpng libtiff libwebp libheif libavif libraw libJXL

Key format coverage:

* **JPEG/JPEG XL** — Photo formats (libjpeg-turbo, libJXL)
* **PNG** — Lossless screenshots, graphics (libpng)
* **WebP** — Web images (libwebp)
* **HEIF/HEIC** — Apple photos format (libheif — requires HEVC decoder)
* **AVIF** — AV1-based image format (libavif)
* **TIFF** — Professional/scientific imaging (libtiff)
* **RAW** — Camera raw formats (libraw — covers CR2, NEF, ARW, DNG, etc.)
* **SVG** — Vector graphics (librsvg, built into GTK)
* **EXR** — HDR imaging (OpenEXR — needed by Blender, GIMP)

Verify Nautilus/Gwenview can generate thumbnails for all formats after installation.

## Hardware-Specific Tools

* [OpenRGB](https://openrgb.org/) — RGB lighting control
* [OpenRazer](https://openrazer.github.io/) — Razer peripheral support
* [linux-surface](https://github.com/linux-surface) — Microsoft Surface support
* [asus-linux](https://asus-linux.org/) — ASUS laptop support
* [MrChromebox](https://docs.mrchromebox.tech/) — Chromebook firmware
* [Asahi Linux](https://asahilinux.org/) — Apple Silicon support
* [t2linux](https://t2linux.org/) — Apple T2 Mac support

## Core Components

* OpenRGB-udev-rules
* rasdaemon

## Monitoring Services

### Log Monitoring
Add users to systemd-journal group on creation

### Hardware Monitoring

    sudo systemctl enable --now smartd
    sudo systemctl enable --now rasdaemon

### Performance Monitoring Tools

* htop
* iotop-c
* nvtop
* iftop
* nethogs
* ss
* powertop
* atop
