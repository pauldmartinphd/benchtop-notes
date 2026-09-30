# Security Architecture

## Principles

* Rolling release patches for fast security updates
* Limited attack surface:
    * Drop all GTK2, Python2
    * Simplified immutable core
* Userspace-only support for:
    * Legacy filesystems
    * File sharing protocols

## Kernel Security

* [KSPP](https://kspp.github.io/) — Kernel Self Protection Project
* [Kicksecure security-misc](https://www.kicksecure.com/wiki/Security-misc) / [GitHub](https://github.com/Kicksecure/security-misc)
* [Clear Linux Security](https://www.clearlinux.org/clear-linux-documentation/guides/clear/security.html)

### Magic SysRq Key

##### /etc/sysctl.d/30-sysrq.conf

	kernel.sysrq = 0

OpenSUSE defaults to 184, which allows sync, remount read-only, reboot/poweroff and debugging dumps from the keyboard.  We turn it off completely.  Root can still use /proc/sysrq-trigger
[Link](https://docs.kernel.org/admin-guide/sysrq.html)

## Firewalls

### Inbound
The combined notes select firewalld for its zones and NetworkManager integration. Earlier notes named ufw; the configuration examples here use firewalld. The desired GUI is `firewall-config` or Cockpit’s firewall panel.

    sudo firewall-cmd --state                     # Check if running
    sudo firewall-cmd --get-default-zone          # Show default zone
    sudo firewall-cmd --list-all                  # Show current rules

For a GUI: `firewall-config` (GTK) or Cockpit's firewall panel.

### Outbound
[OpenSnitch](https://github.com/evilsocket/opensnitch) — Application-level outbound firewall (similar to Little Snitch on macOS). Prompts the user when an application tries to make an outbound connection for the first time. The aim is to make unexpected outbound connections visible to the user.

## Rust Replacements for Security-Critical Tools

* https://discourse.ubuntu.com/t/carefully-but-purposefully-oxidising-ubuntu/56995
* https://www.phoronix.com/news/Ubuntu-25.10-sudo-rs-Default
* https://ubuntu.com/blog/tpm-backed-full-disk-encryption-is-coming-to-ubuntu

## Cryptography and Encryption

### Crypto Policies

* [Ubuntu crypto-config](https://github.com/canonical/crypto-config)
* [Fedora crypto-policies](https://gitlab.com/redhat-crypto/fedora-crypto-policies)
* [OpenSUSE crypto-policies](https://en.opensuse.org/SDB:Crypto-policies)

### Ideas

* fTPM Integration
* YubiKey Integration
* NitroKey Integration

### Disk Encryption

* LUKS Volume Encryption
* Cryptomator Cloud Encryption (encrypts individual files/folders for cloud storage — zero-knowledge encryption)
* CryptSetup Opal (hardware-based self-encrypting drive support via TCG Opal 2.0)

### systemd-cryptenroll
systemd-cryptenroll manages LUKS2 volume key enrollment. It supports:

* **TPM2 binding** — Automatically unlock LUKS volumes when TPM PCR values match (measured boot), without a passphrase
* **FIDO2 tokens** — Unlock with a YubiKey or other FIDO2 security key
* **PKCS#11 tokens** — Unlock with smart cards or hardware security modules
* **Recovery keys** — Generate and enroll a human-readable recovery key as a fallback

Usage examples:

    # Enroll TPM2 (auto-unlock when PCRs match):
    sudo systemd-cryptenroll --tpm2-device=auto --tpm2-pcrs=7+11 /dev/sdXn

    # Enroll a FIDO2 key:
    sudo systemd-cryptenroll --fido2-device=auto /dev/sdXn

    # Generate a recovery key:
    sudo systemd-cryptenroll --recovery-key /dev/sdXn

    # List enrolled keys:
    sudo systemd-cryptenroll /dev/sdXn

PCR selection determines which measurements are checked. PCR 7 records Secure Boot policy; it does not by itself prove that every part of the boot chain is unchanged. The example also selects PCR 11, used by systemd-stub for the unified kernel image and boot-phase measurements. See the [systemd-cryptenroll reference](https://github.com/systemd/systemd/blob/main/man/systemd-cryptenroll.xml) and the recorded TPM issues below.

### TPM Issues

##### Tailscale

* https://news.ycombinator.com/item?id=46531925
* https://github.com/tailscale/tailscale/issues/17654
* https://github.com/tailscale/tailscale/issues/18288
* https://github.com/tailscale/tailscale/issues/18302

##### Aeon

* https://www.reddit.com/r/AeonDesktop/comments/1pwuvnw/pcr15_validation_again_unable_to_reenroll_please/
* https://www.reddit.com/r/AeonDesktop/comments/1o9wip0/the_validation_of_pcr_15_failed/

## polkit Configuration

The intended administrative model is wheel-based access using the invoking user’s credentials. Polkit authorization and sudo authentication are separate controls. The broad rule below is retained from the notes; its action coverage needs review before treating it as the final policy.

##### /polkit-1/rules.d/50-wheel-auth-self.rules

	/* /usr/share/polkit-1/rules.d/50-wheel-auth-self.rules */
	polkit.addRule(function(action, subject) {
	    if (subject.isInGroup("wheel")) {
	        return polkit.Result.AUTH_SELF;
	    }
	});

## Packet Capture for Administrators

Administrators (wheel) capture network traffic with Wireshark without root.  OpenSUSE's permissions profiles let only the wireshark group run dumpcap, and that group has no members unless someone is added to it

##### /usr/share/permissions/packages.d/tc-benchtop-settings.easy (and .secure)

	:package: wireshark
	/usr/bin/dumpcap                                        root:wheel        0750
	 +capabilities cap_net_raw,cap_net_admin=ep

The paranoid profile keeps OpenSUSE's setting.  An entry in /etc/permissions.local still overrides this

Note: permctl reads the .easy and .secure variants only when a base file named after the package (tc-benchtop-settings) exists, even an empty one

## Change to sudo Authentication (from targetpw)

OpenSUSE defaults to `Defaults targetpw` in sudoers, which means `sudo` asks for the **target user's** (root's) password rather than the invoking user's password. The intended Benchtop behavior is to authenticate the invoking administrator instead.

### Fix sudoers

    sudo visudo

Change:

    Defaults targetpw
To:

    # Defaults targetpw   (commented out)

And ensure the wheel group has sudo access:

    %wheel ALL=(ALL) ALL

### Lock the root account
After confirming sudo works with the user's own password:

    sudo passwd -l root

This locks root’s password while retaining wheel-based sudo access. Other login mechanisms, such as SSH keys, are separate configuration decisions.
