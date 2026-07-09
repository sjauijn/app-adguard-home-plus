<p align="center">
  <img src="https://raw.githubusercontent.com/sjauijn/app-adguard-home-plus/main/adguard/icon.png" alt="icon">
</p>

# AdGuard Home Plus

[AdGuard Home][adguard] is a network-wide ad-and-tracker blocking DNS server
with parental control (adult content blocking) capabilities. Its purpose is to
let you control your entire network and all your devices, and it does not
require using a client-side program.

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

## Installation

The installation of this app is pretty straightforward and not different in
comparison to installing any other Home Assistant app.

1. **Ensure your Home Assistant device has a
   [static IP and static external DNS servers!](https://developers.home-assistant.io/docs/operating-system/network)**
   This is important! You **WILL** end up having issues if you skip this step.
   - Change this setting in Network:
     [![Open your Home Assistant instance and manage your systems network configuration.](https://my.home-assistant.io/badges/network.svg)](https://my.home-assistant.io/redirect/network/)
     (_Settings → System → Network
     → Configure network interfaces → Your Interface → IPv4 → Static_)
   - Please note, setting a fixed IP in your router is **NOT** static.

2. Click to add the stable repository:
   [![Add Stable Repository](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https://github.com/sjauijn/app-adguard-home-plus)

   Or manually add:

   ```text
   https://github.com/sjauijn/app-adguard-home-plus
   ```

## Configuration

**Note**: _Remember to restart the app when the configuration is changed._

Example app configuration:

```yaml
log_level: info
ssl: true
certfile: fullchain.pem
keyfile: privkey.pem
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### AdGuardHome.yaml location

The main AdGuard Home configuration file is stored at:

```
/addon_configs/adguard/AdGuardHome.yaml
```

This path is accessible via SFTP (e.g. using WinSCP, Cyberduck, or the
VS Code Remote SSH extension) without needing Portainer or Docker console
access. Runtime data (query log, statistics, filter databases) remains in
`/data/adguard/` as in the original app.

### Option: `log_level`

The `log_level` option controls the level of log output by the app and can
be changed to be more or less verbose, which might be useful when you are
dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `notice`: Normal but significant events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. App becomes unusable.

Please note that each level automatically includes log messages from a
more severe level, e.g., `debug` also shows `info` messages. By default,
the `log_level` is set to `info`, which is the recommended setting unless
you are troubleshooting.

### Option: `ssl`

Enables/Disables SSL (HTTPS) on the app. Set it `true` to enable it,
`false` otherwise.

**Note**: _The SSL settings only apply to direct access and has no effect
on the Ingress service._

### Option: `certfile`

The certificate file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `keyfile`

The private key file to use for SSL.

**Note**: _The file MUST be stored in `/ssl/`, which is the default_

### Option: `leave_front_door_open`

Adding this option to the app configuration allows you to disable
authentication on the AdGuard Home by setting it to `true`.

**Note**: _We STRONGLY suggest, not to use this, even if this app is
only exposed to your internal network. USE AT YOUR OWN RISK!_

## Encryption Settings (Advanced Usage)

AdGuard Home allows the configuration of running DNS-over-HTTPS and
DNS-over-TLS locally. If you configure these options please ensure to restart
the app afterwards. Also to use DNS-over-HTTPS correctly please ensure to
configure SSL on the app as well as in AdGuard Home itself. Also consider
that the app and AdGuard Home cannot use the same port for SSL.

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_adguard&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[adguard]: https://adguard.com/adguard-home/overview.html
