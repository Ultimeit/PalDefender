# 📁 File Types

**PalDefender** supports a range of custom file types that can be used to configure your server’s behavior and extend its features.
Currently supported:
* `Config.json`
* `WhiteList.json`
* `Banlist.json` <span class='pd-badge pd-badge--beta'>Beta</span>
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json` <span class='pd-badge pd-badge--beta'>Beta</span>
* `RESTAPI/RESTConfig.json` <span class='pd-badge pd-badge--beta'>Beta</span>
* `RESTAPI/Tokens/*.json` <span class='pd-badge pd-badge--beta'>Beta</span>

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

### 🚫 `Banlist.json` <span class='pd-badge pd-badge--beta'>Beta</span>

Stores PalDefender ban records used by ban, unban, IP-ban, and REST punishment tools.

* Prefer `/ban`, `/unban`, `/banip`, `/unbanip`, or the REST API instead of editing this file manually.
* If you must edit it manually, stop the server first or reload configuration after changes.

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Used for spawning or giving customized Pals via commands.

* Defines the Pal’s **ID, nickname, gender, stats (HP/SP/MP), hunger, sanity, shiny status, skills, IVs, passives**, and more.
* Allows full customization of a Pal’s **combat, utility, and work traits**.

---

### 📍 [PalSummon.json](./PalSummon.md)

Spawns a custom Pal at a specific location.

* References a `PalTemplate`, sets **world position (X, Y, Z)**.
* Configures flags such as **uncapturable** and disables specific **status effects** (e.g., poison, drowning, burn, etc.).

---

### 🧾 [Pals/ImportRules/*.json](./PalImportRules.md) <span class='pd-badge pd-badge--beta'>Beta</span>

Controls how custom Pal templates are accepted.

* Set global limits in `Pals/ImportRules/Default.json`.
* Add per-Pal overrides with files such as `Pals/ImportRules/Anubis.json`.
* Choose whether over-limit values are blocked or clamped.
* Choose whether disallowed passives block imports or are removed.

---

### 🌐 REST API config files <span class='pd-badge pd-badge--beta'>Beta</span>

REST API configuration lives in `RESTAPI/RESTConfig.json`, while bearer tokens live in `RESTAPI/Tokens/*.json`.

* `RESTConfig.json` controls whether the API is enabled, the bind address, port, console logging, and CORS settings.
* Each token file should contain a private token and permissions. Do not share token values publicly.
