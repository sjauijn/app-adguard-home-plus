# AdGuard Home Plus - Original HA Community App + AdGuardHome.yaml via "/addon_configs"

Network-wide ads & trackers blocking DNS server.

![The AdGuard Home Home Assistant App](https://github.com/sjauijn/app-adguard-home-plus/blob/main/images/screenshot.png)

## About

AdGuard Home is a network-wide ad-and-tracker blocking DNS server with
parental control (adult content blocking) capabilities. Its purpose is to let
you control your entire network and all your devices, and it does not require
using a client-side program.

AdGuard Home provides a beautiful, easy and feature-rich web interface to
easily manage the filtering process and its settings.

## What's different from the original app

This fork moves `AdGuardHome.yaml` from the internal `/data/adguard/` directory
to `/addon_configs/adguard/`, making it accessible via SFTP without needing
Portainer or Docker console access.

| | Original | This fork |
|---|---|---|
| `AdGuardHome.yaml` location | `/data/adguard/` | `/addon_configs/adguard/` |
| Accessible via SFTP | ❌ | ✅ |
| Query log, stats, filters DB | `/data/adguard/` | `/data/adguard/` (unchanged) |

**Migration**: On first start, if you already have an existing config in
`/data/adguard/AdGuardHome.yaml`, it will be automatically copied to the new
location. The old file will be renamed to `AdGuardHome.yaml.bak`.
