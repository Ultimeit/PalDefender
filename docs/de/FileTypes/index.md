# 📁 Dateitypen

**PalDefender** unterstützt verschiedene benutzerdefinierte Dateitypen, mit denen du das Serververhalten konfigurierst und Funktionen erweiterst.
Derzeit unterstützt:
* `Config.json`
* `WhiteList.json`
* `Banlist.json`
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json`
* `RESTAPI/RESTConfig.json`
* `RESTAPI/Tokens/*.json`

---

## ⚡ Schnellübersicht

### 🛠️ [Config.json](./Config.md)

Steuert Serververhalten, Moderation, Protokollierung und Administratoreinstellungen.

* **Sicherheit:** Anti-Cheat (Warnung, Kick, Sperre, IP-Sperre), Namens-/Wortfilter, SteamID-Schutz und Prüfung unzulässiger Werte oder Gegenstände.
* **Protokollierung:** Erfasst Chat, RCON, Anmeldungen, Tode, Beschwörungen, Bauaktivitäten und Oil-Rig-Ereignisse.
* **Administration:** IP-Freigabeliste, automatische Anmeldung, Godmode/Cheats und Sichtbarkeit von Administratoraktionen.
* **Ankündigungen:** MOTD, Spielertode, Beschwörungen, Strafen und Beuteereignisse.
* **Chat- und Spiellimits:** Nachrichtenlänge, Umgehung von Abklingzeiten, PvP-/PvE-Schadensgrenzen und Baumfälllimit.
* **Sonstiges:** Base64-Unterstützung für RCON, Behandlung von Startfehlern und optionaler chinesischer Befehlsmodus.

---

### 👥 `WhiteList.json`

Legt fest, wer dem Server beitreten darf.
Unterstützt sowohl **Benutzer-IDs** als auch **IP-Adressen** einschließlich maskierter Bereiche.

---

### 🚫 `Banlist.json`

Speichert PalDefender-Sperreinträge, die von Sperr-, Entsperr-, IP-Sperr- und REST-Sanktionswerkzeugen verwendet werden.

* Verwende vorzugsweise `/ban`, `/unban`, `/banip`, `/unbanip` oder die REST-API, statt diese Datei manuell zu bearbeiten.
* Wenn du sie manuell bearbeiten musst, stoppe zuerst den Server oder lade die Konfiguration nach der Aenderung neu.

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Wird verwendet, um angepasste Pals über Befehle zu erzeugen oder zu vergeben.

* Definiert **ID, Spitzname, Geschlecht, Werte (HP/SP/MP), Hunger, Verstand, Seltenheitsstatus, Skills, IVs, Passives** und weitere Eigenschaften des Pals.
* Erlaubt vollständige Anpassung der **Kampf-, Nutz- und Arbeitswerte** eines Pals.

---

### 📍 [PalSummon.json](./PalSummon.md)

Erzeugt einen angepassten Pal an einer bestimmten Position.

* Verweist auf ein `PalTemplate` und setzt die **Weltposition (X, Y, Z)**.
* Konfiguriert Merkmale wie **nicht fangbar** und deaktiviert bestimmte **Statuseffekte** (z. B. Gift, Ertrinken oder Verbrennung).

---

### 🧾 [Pals/ImportRules/*.json](./PalImportRules.md)

Steuert, wie benutzerdefinierte Pal-Templates angenommen werden.

* Setze globale Limits in `Pals/ImportRules/Default.json`.
* Füge Pal-spezifische Überschreibungen mit Dateien wie `Pals/ImportRules/Anubis.json` hinzu.
* Lege fest, ob Werte oberhalb der Limits blockiert oder reduziert werden.
* Lege fest, ob unerlaubte Passives den Import blockieren oder entfernt werden.

---

### 🌐 REST-API-Konfigurationsdateien

Die REST-API-Konfiguration befindet sich in `RESTAPI/RESTConfig.json`; Bearer-Token liegen in `RESTAPI/Tokens/*.json`.

* `RESTConfig.json` steuert, ob die API aktiviert ist, sowie Bind-Adresse, Port, Konsolenprotokollierung und CORS-Einstellungen.
* Jede Token-Datei sollte ein privates Token und Berechtigungen enthalten. Veröffentliche Tokenwerte niemals.
