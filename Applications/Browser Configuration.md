# Browser Configuration

## Brave (Default Browser)

The selected policy disables Rewards, Wallet, VPN, AI Chat, and Tor, and leaves DNS-over-HTTPS in automatic mode:

```json
{
    "BraveRewardsDisabled": true,
    "BraveWalletDisabled": true,
    "BraveVPNDisabled": 1,
    "BraveAIChatEnabled": false,
    "TorDisabled": true,
    "DnsOverHttpsMode": "automatic"
}
```

## Firefox

### Fix Scrolling

    apz.gtk.pangesture.delta_mode=2
    apz.gtk.pangesture.pixel_delta_mode_multiplier=25
[Bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1752862)

### Switch Browser Cache from Disk (SSD) to RAM

    browser.cache.disk.enable=false
    browser.cache.disk_cache_ssl=false

### Font Selection
#TODO

### Browser Cache
#TODO — Investigate optimal cache settings
