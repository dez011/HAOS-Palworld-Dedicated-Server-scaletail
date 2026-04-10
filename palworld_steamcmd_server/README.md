# 🦖 Palworld Dedicated Server (SteamCMD)

![Home Assistant OS](https://img.shields.io/badge/Home%20Assistant-OS-blue)
![Architecture](https://img.shields.io/badge/Architecture-amd64-blue)
![SteamCMD](https://img.shields.io/badge/SteamCMD-Enabled-orange)
![Tailscale](https://img.shields.io/badge/Tailscale-Optional-blueviolet)
![Status](https://img.shields.io/badge/Status-Beta-orange)

A Home Assistant OS add-on to run a fully host-based **Palworld Dedicated Server**
using **SteamCMD**, with optional **Tailscale** integration for zero-config networking.

---

## 🚀 Overview

This add-on runs a **Palworld Dedicated Server** directly on **Home Assistant OS**.

All data is stored entirely on the host under `/share`, including:

- SteamCMD
- Palworld server files
- Configuration
- Savegames

No additional server, virtual machine, or external host is required.

---

## ✨ Features

- Official Palworld Dedicated Server (Steam App ID `2394010`)
- Automatic updates via SteamCMD
- Persistent data storage under `/share`
- Runs directly on Home Assistant OS
- Easy installation via the Home Assistant Add-on Store
- **Optional Tailscale VPN** – no port-forwarding needed, players on your Tailnet connect directly

---

## 📦 Installation

1. Open **Home Assistant**
2. Go to **Settings → Add-ons → Add-on Store**
3. Add the following repository:

```
https://github.com/dez011/HAOS-Palworld-Dedicated-Server-scaletail
```

4. Install **Palworld Dedicated Server (Tailscale)**
5. Start the add-on

---

## 📁 Data Location

All server data is stored persistently under:

```text
/share/palworld/
├── server/      ← Palworld server files
├── config/      ← Configuration files
├── steam_home/  ← SteamCMD home directory
└── tailscale/   ← Tailscale state (if enabled)
```

You can access this directory from Windows via:

```
\\<HOME_ASSISTANT_IP>\share\palworld\
```

---

## 🎮 Server Configuration

Server configuration is done via configuration files.

Main configuration file:

```
/share/palworld/config/PalWorldSettings.ini
```

After editing the configuration file, restart the add-on for changes to take effect.

---

## 🌐 Network Ports

| Port  | Protocol | Description  |
|-------|----------|--------------|
| 8211  | UDP      | Game server  |
| 27015 | UDP      | Query port   |

Make sure these ports are forwarded on your router if you want external players to join **without** Tailscale.

> **With Tailscale enabled**, players on your Tailnet can connect directly using the Tailscale IP or hostname – **no port-forwarding required**.

---

## ⚙️ Add-on Options

### General

| Option           | Type   | Default     | Description                                      |
|------------------|--------|-------------|--------------------------------------------------|
| `app_id`         | int    | `2394010`   | Steam App ID for Palworld Dedicated Server       |
| `steam_user`     | string | `anonymous` | Steam username (anonymous for free games)        |
| `steam_pass`     | string | *(empty)*   | Steam password (leave empty for anonymous)       |
| `update_on_boot` | bool   | `true`      | Automatically update the server on add-on start  |

### 🔗 Tailscale (Optional)

Enable Tailscale to expose your Palworld server on your private Tailnet without opening any ports on your router.

| Option                          | Type   | Default                     | Description                                                                 |
|---------------------------------|--------|-----------------------------|-----------------------------------------------------------------------------|
| `tailscale_enabled`             | bool   | `false`                     | Enable or disable Tailscale VPN                                            |
| `tailscale_authkey`             | string | *(empty)*                   | **Required when enabled.** A Tailscale auth key from your admin console    |
| `tailscale_hostname`            | string | `palworld`                  | Hostname shown in your Tailnet (e.g. `palworld`)                           |
| `tailscale_accept_dns`          | bool   | `true`                      | Accept DNS settings from Tailscale (MagicDNS)                              |
| `tailscale_advertise_exit_node` | bool   | `false`                     | Advertise this node as a Tailscale exit node                               |
| `tailscale_funnel`              | bool   | `false`                     | Enable Tailscale Funnel (TCP-only, not useful for game UDP traffic)        |
| `tailscale_state_dir`           | string | `/share/palworld/tailscale` | Directory to persist Tailscale state across restarts                       |

### How to set up Tailscale

1. Go to [Tailscale Admin Console → Settings → Keys](https://login.tailscale.com/admin/settings/keys)
2. Generate a new **Auth Key** (reusable recommended, or one-time)
3. In the add-on configuration, set:
   - `tailscale_enabled`: **true**
   - `tailscale_authkey`: paste your auth key
   - `tailscale_hostname`: e.g. `palworld`
4. Start (or restart) the add-on
5. Your server will appear on your Tailnet. Players connect using:
   ```
   <tailscale-ip>:8211
   ```
   or if MagicDNS is enabled:
   ```
   palworld:8211
   ```

> **Note:** All players must be on your Tailnet (have Tailscale installed and logged in to the same network) to connect via the Tailscale IP.

---

## ❤️ Support & Donations

This project is developed and maintained in my free time.

If you enjoy this add-on and find it useful,
I would really appreciate a small donation to support my work and ongoing development.

👉 [Donate via PayPal](http://paypal.me/cyclemat)

Donations are completely optional – thank you very much!

---

## 🧑‍💻 Maintainer

**Author:** CyCleMat

**GitHub:** [https://github.com/cyclemat](https://github.com/cyclemat)

---

## 📜 Disclaimer

This add-on is not affiliated with or endorsed by Pocketpair or Palworld developers.
All trademarks and game content belong to their respective owners.
