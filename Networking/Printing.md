# Printing (IPP Driverless Only)

## Intended support

Use driverless printing through CUPS, with IPP Everywhere, AirPrint, and Mopria-capable devices as the target. These are related driverless-printing standards built around IPP; they are not interchangeable certifications. Common job formats include PDF, PWG Raster, Apple Raster, and PCLm, depending on the device. Discovery uses DNS-SD/mDNS. See [OpenPrinting’s driverless overview](https://openprinting.github.io/driverless).

The proposed stack is CUPS, the required filters, Avahi discovery, and ipp-usb for devices that implement IPP-over-USB. It should cover compatible printers used from Apple, Windows, ChromeOS, and Android environments. A printer’s age or enterprise branding alone does not establish compatibility. Microsoft’s IPP class-driver approach and Mopria are references for the intended interoperability.

The design avoids shipping large vendor-specific driver collections by default. Unsupported older printers or device-specific finishing and accounting functions may still need another solution.

## Package candidates

Resolve the package names against the image’s selected repositories before adding them to the pattern.

### Core Printing (CUPS with IPP Everywhere)

* cups
* cups-filters
* cups-filters-ipp
* cups-filters-ghostscript
You do not need Gutenprint or PPD collections if you are strictly driverless.

### Discovery (AirPrint / Mopria)

* avahi
* avahi-utils
Avahi provides Bonjour/mDNS service advertisements and discovery.

### IPP over USB

* ipp-usb
Exposes a local IPP service for compatible USB printers and MFPs. It requires device support for IPP-over-USB; ordinary USB connectivity is not enough. See the [ipp-usb manual](https://github.com/OpenPrinting/ipp-usb/blob/master/ipp-usb.8.md).

## Packages NOT Needed

* No HPLIP
* No Epson ESC/P-R
* No Canon UFR2
* No Brother LPR
* No foomatic-db
* No PPD packs
* No proprietary filters

## Enable CUPS

    sudo systemctl enable --now cups

## Driverless Scanning

Modern MFPs (multifunction printers) support driverless scanning via two protocols:

### eSCL (AirScan)
eSCL is Apple's scanning protocol (part of AirPrint). Most modern MFPs support it. On Linux, use the `sane-airscan` backend:

    sudo zypper install sane-airscan

This provides a SANE backend (`airscan`) that auto-discovers eSCL-capable scanners via mDNS. Test discovery and scanning with GNOME Document Scanner (`simple-scan`) or another SANE client on the supported devices.

### WSD (Web Services for Devices)
WSD is Microsoft's discovery and scanning protocol. Some corporate/enterprise scanners only support WSD and not eSCL. The `sane-airscan` backend also supports WSD scanning.

### Packages

    sudo zypper install sane-backends sane-airscan simple-scan

### Verification

    scanimage -L          # List detected scanners
    # Should show something like:
    # device `airscan:e0:HP LaserJet MFP M234dw' is a eSCL HP LaserJet MFP M234dw ip=192.168.1.x

### Packages NOT Needed for Driverless Scanning

* No HPLIP (hp-scan)
* No iscan (Epson)
* No brscan (Brother)
* No vendor-specific SANE backends

Note: Some older scanners (pre-2015) may not support eSCL or WSD and will still require vendor-specific SANE backends. The recorded plan includes `sane-backends` as a fallback while avoiding vendor software bundles by default.
