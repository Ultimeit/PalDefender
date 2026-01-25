# 🛠️ Config.json

| Config Key                     | Typ    | Beschreibung                                                                 |
| ------------------------------ | ------ | ----------------------------------------------------------------------------- |
| `version`                      | string | Versionskennung der Konfiguration (z. B. `"1.0.0"`).                          |
| `MOTD`                         | array  | Nachricht des Tages (Message of the Day). Unterstützt Platzhalter:<br>`{ServerName}` -> String – Name des Servers<br>`{PlayerName}` -> String – Spieler, der beigetreten ist<br>`{Difficulty}` -> String – falls in der Palworld-.ini gesetzt<br>`{DeathPenalty}` -> String<br>`{AllowGlobalPalboxExport}` -> "Enabled" / "Disabled"<br>`{AllowGlobalPalboxImport}` -> "Enabled" / "Disabled"<br>`{IsPvP}` -> "Enabled" / "Disabled"<br>`{IsHardcore}` -> "Enabled" / "Disabled"<br>`{FriendlyFire}` -> "Enabled" / "Disabled"<br>`{DayTimeSpeedRate}` -> Float-Zahl<br>`{NightTimeSpeedRate}` -> Float-Zahl<br>`{ExpRate}` -> Float-Zahl<br>`{PalCaptureRate}` -> Float-Zahl<br>`{PalSpawnNumRate}` -> Float-Zahl<br>`{PalEggDefaultHatchingTime}` -> Float-Zahl<br>`{EnemyDropItemRate}` -> Float-Zahl<br>`{PalStomachDecreaceRate}` -> Float-Zahl<br>`{PalStaminaDecreaceRate}` -> Float-Zahl<br>`{BaseCampMaxNumInGuild}` -> Int-Zahl<br>`{SupplyDropSpan}` -> Int-Zahl<br>`{MaxBuildingLimitNum}` -> Int-Zahl<br> |
| `exitServerOnStartupFailure`   | bool   | Wenn `true`, wird der Server heruntergefahren, falls PalDefender nicht starten kann. Sinnvoll zum Schutz des Savegames vor einem Betrieb ohne PalDefender. **Kann bei manchen Server-Hostern Probleme verursachen, wenn Exit-Codes nicht geprüft werden und ein Absturzloop entsteht.** |
| `preventAdminPasswordInChat`   | bool   | Verhindert, dass Admin-Passwörter im Chat sichtbar werden. Hat keine Wirkung, wenn kein Admin-Passwort gesetzt ist. |
| `shouldWarnCheaters`           | bool   | Sendet eine Warnmeldung an erkannte Cheater, sobald sie entdeckt wurden.     |
| `shouldWarnCheatersReason`     | bool   | Fügt der Cheater-Warnmeldung den Erkennungsgrund hinzu.                       |
| `shouldKickCheaters`           | bool   | Kickt erkannte Cheater automatisch vom Server.                               |
| `shouldBanCheaters`            | bool   | Bannt erkannte Cheater automatisch.                                          |
| `shouldIPBanCheaters`          | bool   | IP-bannd erkannte Cheater automatisch.                                       |
| `RCONTimeout`                  | float  | Legt das Timeout fest, nach dem eine RCON-Verbindung getrennt wird.          |
| `RCONUsePacketIdFix`           | bool   | Behebt fehlerhafte Paket-IDs durch eine falsche Implementierung der RCON-Paketverarbeitung von Pocketpair. |
| `logNetworking`                | bool   | Protokolliert eingehende Netzwerkdaten von Clients.                          |
| `logNetworkingToConsole`       | bool   | Gibt Netzwerkverkehr zusätzlich in der Konsole aus.                          |
| `logChat`                      | bool   | Protokolliert alle Chat-Nachrichten von Spielern.                            |
| `logRCON`                      | bool   | Protokolliert die Nutzung von RCON-Befehlen.                                 |
| `logPlayerUID`                 | bool   | Protokolliert die PlayerUID von Spielern in relevanten Logs.                 |
| `logPlayerIP`                  | bool   | Protokolliert die IP-Adresse von Spielern in relevanten Logs.                |
| `logPlayerDeaths`              | bool   | Protokolliert Spielertode.                                                   |
| `logPlayerLogins`              | bool   | Protokolliert Spieler-Login- und Logout-Ereignisse.                          |
| `logPlayerBuildings`           | bool   | Protokolliert Bauaktionen von Spielern (Bauen, Abbrechen, Abbauen).          |
| `logHelicopterKills`           | bool   | Protokolliert Kills durch Helikopter.                                        |
| `logPlayerSummons`             | bool   | Protokolliert Pal-Beschwörungen durch Spieler.                               |
| `logPlayerCaptures`            | bool   | Protokolliert Pal-Fänge durch Spieler.                                       |
| `logCraftings`                 | bool   | Protokolliert Crafting-Aktivitäten von Spielern.                             |
| `logTechUnlocks`               | bool   | Protokolliert freigeschaltete Technologien von Spielern.                    |
| `logOpenOilrigBoxes`           | bool   | Protokolliert Interaktionen mit Ölplattform-Kisten.                          |
| `OilrigGoalBoxLocktime`        | int    | Zeit in Sekunden, wie lange die Zielkiste der Ölplattform gesperrt bleibt (Standard: `300`). |
| `useAdminWhitelist`            | bool   | Aktiviert die Admin-IP-Whitelist. **Die IPs müssen in `adminIPs` gesetzt sein!** |
| `adminAutoLogin`               | bool   | Meldet freigeschaltete Admins beim Betreten automatisch im Admin-Modus an.   |
| `adminIPs`                     | array  | Liste der IP-Adressen, die Admin-Befehle ausführen dürfen.                   |
| `bannedIPs`                    | array  | Liste gesperrter IP-Adressen.                                                |
| `bannedChatWords`              | array  | Chat-Filter für gesperrte Wörter (z. B. RMT-Werbung).                        |
| `bannedMessage`                | string | Nachricht, die gebannten Spielern angezeigt wird.                           |
| `bannedNames`                  | array  | Verbotene Spielernamen (z. B. aus gecrackten Versionen).                     |
| `pvpMaxToBuildingDamage`       | int    | Maximal erlaubter PvP-Schaden an Gebäuden.                                   |
| `pvpMaxToPalDamage`            | int    | Maximal erlaubter PvP-Schaden an Pals.                                       |
| `pveMaxToPalBanThreshold`      | int    | PvE-Schadensgrenze an Pals, ab der Cheat-Erkennung ausgelöst wird.           |
| `treeLimiter`                  | float  | Maximale Zeit, die ein Spieler zum Zerstören eines Baumes benötigt (z. B. `0.1` = 1 Baum pro 100 ms). Verhindert starke Lags bei Massenschaden (z. B. Raketen). |
| `allowAdminCheats`             | bool   | Erlaubt Admins die Nutzung von Cheat-Befehlen wie Godmode.                   |
| `allowGodmodeOnehit`           | bool   | Ermöglicht One-Hit-Kills im Godmode.                                         |
| `adminCheats`                  | array  | Definiert, welche Befehle als Admin-Cheats gelten. Wenn Admin-Cheats deaktiviert sind, können diese Befehle nicht von Admins ausgeführt werden (RCON weiterhin erlaubt). |
| `isChineseCmd`                 | bool   | Aktiviert chinesische Zeichenkodierung in der Konsole (Legacy).              |
| `announceConnections`          | bool   | Kündigt Spieler-Beitritte und -Verlassen im Chat an.                        |
| `dontAnnounceAdminConnections` | bool   | Unterdrückt Verbindungsnachrichten für Admins.                               |
| `announcePunishments`          | bool   | Kündigt Cheat-Bans/Kicks im Chat an.                                         |
| `announcePlayerDeaths`         | bool   | Zeigt öffentliche Todesmeldungen im Chat an.                                 |
| `announceOpenOilrigBoxes`      | bool   | Kündigt Loot-Ereignisse von Ölplattformen im Chat an.                        |
| `announceHelicopterKills`      | bool   | Kündigt Helikopter-Kills im Chat an.                                         |
| `announcePlayerSummons`        | bool   | Kündigt Pal-Beschwörungen von Spielern im Chat an.                           |
| `announceAdminSummons`         | bool   | Kündigt Pal-Beschwörungen durch Admin-Befehle im Chat an.                   |
| `announceAdminSummonsKill`     | bool   | Kündigt an, wenn ein Spieler einen durch Admins beschworenen Pal tötet.     |
| `chatBypassWait`               | bool   | Entfernt die Abklingzeit zwischen Chat-Nachrichten.                          |
| `chatMessageMaxLen`            | int    | Maximale Länge von Chat-Nachrichten.                                         |
| `useWhitelist`                 | bool   | Aktiviert `WhiteList.json`.                                                  |
| `whitelistMessage`             | string | Nachricht für Spieler, die nicht auf der Whitelist stehen.                  |
| `steamidProtection`            | bool   | Verhindert doppelte Logins mit derselben UserId.                             |
| `blockTowerBossCapture`        | bool   | Deaktiviert das Fangen von Turmbossen.                                       |
| `RCONbase64`                   | bool   | Aktiviert Base64-kodierte RCON-Befehle.                                      |
| `disableIllegalItemProtection` | bool   | Deaktiviert den Schutz vor modifizierten Items (z. B. Debug-Sphären).       |
| `disableButchering`            | bool   | Deaktiviert das Schlachten.                                                  |
| `disableRenaming`              | bool   | Deaktiviert das Umbenennen von Charakteren.                                  |
| `disablePalRenaming`           | bool   | Deaktiviert das Umbenennen von Pals.                                         |
| `doActionUponIllegalPalStats`  | bool   | Reagiert automatisch auf illegale Pal-Stat-Exploits.                        |
| `palStatsMaxRank`              | int    | Maximal erlaubter Pal-Verbesserungsrang (`-1` = automatische Erkennung).    |
| `bannedTechnologies`           | array  | Blockiert Technologien. Diese werden beim Beitritt automatisch verlernt.   |
