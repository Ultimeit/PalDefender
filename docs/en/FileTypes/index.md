# 📁 File Types

**PalDefender** supports a range of custom file types that can be used to configure your server’s behavior and extend its features.
Currently supported:
* `Config.json`
* `WhiteList.json`
* `PalTemplate.json`
* `PalSummon.json`

---

## ⚡ Quick Overview

### 🛠️ [Config.json](./Config.md)

Controls server behavior, moderation, logging, and admin settings.

* **Security:** Anti-cheat (warn, kick, ban, IP-ban), name/word filtering, SteamID protection, illegal stat/item checks.
* **Logging:** Tracks chat, RCON, logins, deaths, summons, building activity, oilrig events.
* **Admin:** IP whitelisting, auto-login, godmode/cheats, visibility of admin actions.
* **Announcements:** MOTD, player deaths, summons, punishments, and loot events.
* **Chat & Gameplay Limits:** Message length, cooldown bypass, PvP/PvE damage caps, tree cutting limit.
* **Misc:** RCON base64 support, startup failure handling, optional Chinese command mode.

---

### 👥 `WhiteList.json`

Defines who is allowed to join the server.
Supports both **User IDs** and **IP addresses** (including masked ranges).

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Used for spawning or giving customized Pals via commands.

* Defines the Pal’s **ID, nickname, gender, stats (HP/SP/MP), hunger, sanity, shiny status, skills, IVs, passives**, and more.
* Allows full customization of a Pal’s **combat, utility, and work traits**.

---

### 📍PalSummon.json` [PalSummon.json](./PalSummon.md)

Spawns a custom Pal at a specific location.

* References a `PalTemplate`, sets **world position (X, Y, Z)**.
* Configures flags such as **uncapturable** and disables specific **status effects** (e.g., poison, drowning, burn, etc.).
