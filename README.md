<p align="center">
  <img src="https://raw.githubusercontent.com/sjauijn/app-adguard-home-plus/main/adguard/icon.png" alt="icon">
</p>

# AdGuard Home Plus

Network-wide ads & trackers blocking DNS server.


## About

AdGuard Home is a network-wide ad-and-tracker blocking DNS server with
parental control (adult content blocking) capabilities. Its purpose is to let
you control your entire network and all your devices, and it does not require
using a client-side program.

AdGuard Home provides a beautiful, easy and feature-rich web interface to
easily manage the filtering process and its settings.

![The AdGuard Home Home Assistant App](https://github.com/sjauijn/app-adguard-home-plus/blob/main/images/screenshot.png)

## Installation

1. Click to add the stable repository:
   [![Add Stable Repository](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https://github.com/sjauijn/app-adguard-home-plus)

2. Or manually add:

   ```text
   https://github.com/sjauijn/app-adguard-home-plus
   ```



## What's different from the original app

This fork moves `AdGuardHome.yaml` from the internal `/data/adguard/` directory
to `/addon_configs/adguard/`, making it accessible via SFTP without needing
Portainer or Docker console access.

| | Original | This fork |
|---|---|---|
| `AdGuardHome.yaml` location | `/data/adguard/` | `/addon_configs/adguard/` |
| Accessible via SFTP | ❌ | ✅ |
| Query log, stats, filters DB | `/data/adguard/` | `/data/adguard/` (unchanged) |
