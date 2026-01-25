# 📁 Dateitypen

**PalDefender** unterstützt eine Reihe benutzerdefinierter Dateitypen, mit denen das Serververhalten konfiguriert und die Funktionalität erweitert werden kann.
Derzeit unterstützt:

* `Config.json`
* `WhiteList.json`
* `PalTemplate.json`
* `PalSummon.json`

---

## ⚡ Kurzübersicht

### 🛠️ [Config.json](./Config.md)

Steuert das Serververhalten, Moderation, Logging und Admin-Einstellungen.

* **Sicherheit:** Anti-Cheat (Warnen, Kicken, Bannen, IP-Bann), Namen-/Wortfilter, SteamID-Schutz, Prüfungen auf illegale Stats/Items.
* **Logging:** Protokolliert Chat, RCON, Logins, Tode, Beschwörungen, Bauaktivitäten und Ölplattform-Ereignisse.
* **Admin:** IP-Whitelist, Auto-Login, Godmode/Cheats, Sichtbarkeit von Admin-Aktionen.
* **Ankündigungen:** MOTD, Spielertode, Beschwörungen, Bestrafungen und Loot-Ereignisse.
* **Chat- & Gameplay-Limits:** Nachrichtenlänge, Cooldown-Bypass, PvP-/PvE-Schadenslimits, Baumfäll-Limit.
* **Sonstiges:** RCON-Base64-Unterstützung, Verhalten bei Startfehlern, optionaler chinesischer Befehlsmodus.

---

### 👥 `WhiteList.json`

Definiert, wer dem Server beitreten darf.
Unterstützt sowohl **User-IDs** als auch **IP-Adressen** (inklusive maskierter Bereiche).

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Wird verwendet, um über Befehle individuell konfigurierte Pals zu spawnen oder zu vergeben.

* Definiert **ID, Spitznamen, Geschlecht, Statuswerte (HP/SP/MP), Hunger, Sanity, Shiny-Status, Skills, IVs, Passive Skills** und mehr.
* Ermöglicht die vollständige Anpassung der **Kampf-, Utility- und Arbeitsfähigkeiten** eines Pals.

---

### 📍 `PalSummon.json` [PalSummon.json](./PalSummon.md)

Spawnt einen benutzerdefinierten Pal an einer festen Position.

* Verwendet ein `PalTemplate` und setzt die **Weltposition (X, Y, Z)**.
* Konfiguriert Flags wie **nicht fangbar** und deaktiviert bestimmte **Statuseffekte** (z. B. Gift, Ertrinken, Verbrennen usw.).
