# :octicons-tools-16: Config.json

| Config-Schlüssel                     | Typ   | Beschreibung                                                               |
| ------------------------------ | ------ | ------------------------------------------------------------------------- |
| `version`                      | string | Versionskennung der Config (z. B. `"1.0.0"`). |
| `MOTD`                         | array  | Message of the Day. Unterstützt Platzhalter:<br>`{ServerName}` -> String - Servername<br>`{PlayerName}` -> String - beigetretener Spieler<br>`{Difficulty}` -> String - falls in der Palworld-INI gesetzt<br>`{DeathPenalty}` -> String<br>`{AllowGlobalPalboxExport}` -> "Enabled" / "Disabled"<br>`{AllowGlobalPalboxImport}` -> "Enabled" / "Disabled"<br>`{IsPvP}` -> "Enabled" / "Disabled"<br>`{IsHardcore}` -> "Enabled" / "Disabled"<br>`{FriendlyFire}` -> "Enabled" / "Disabled"<br>`{DayTimeSpeedRate}` -> Float-Zahl<br>`{NightTimeSpeedRate}` -> Float-Zahl<br>`{ExpRate}` -> Float-Zahl<br>`{PalCaptureRate}` -> Float-Zahl<br>`{PalSpawnNumRate}` -> Float-Zahl<br>`{PalEggDefaultHatchingTime}` -> Float-Zahl<br>`{EnemyDropItemRate}` -> Float-Zahl<br>`{PalStomachDecreaceRate}` -> Float-Zahl<br>`{PalStaminaDecreaceRate}` -> Float-Zahl<br>`{BaseCampMaxNumInGuild}` -> Int-Zahl<br>`{SupplyDropSpan}` -> Int-Zahl<br>`{MaxBuildingLimitNum}` -> Int-Zahl<br> |
| `exitServerOnStartupFailure`   | bool   | Wenn `true`, wird der Server beendet, wenn PalDefender nicht starten kann. Das schützt deinen Spielstand davor, ohne PalDefender zu laufen. **Kann bei manchen Server-Hosts Probleme verursachen, wenn Exit Codes nicht geprüft werden und ein Crash angenommen wird, wodurch eine Endlosschleife entstehen kann.** |
| `preventAdminPasswordInChat`   | bool   | Verhindert, dass Admin-Passwörter im Chat geleakt werden. Hat keine Wirkung, wenn kein Admin-Passwort gesetzt ist. |
| `shouldWarnCheaters`           | bool   | Sendet ertappten Cheatern eine Warnmeldung.        |
| `shouldWarnCheatersReason`     | bool   | Fügt der Cheater-Warnmeldung oben den Grund hinzu. |
| `shouldKickCheaters`           | bool   | Kickt erkannte Cheater automatisch. |
| `shouldBanCheaters`            | bool   | Bannt erkannte Cheater automatisch. |
| `shouldIPBanCheaters`          | bool   | Verhängt automatisch IP-Banns gegen erkannte Cheater. |
| `RCONTimeout`                  | float  | Timeout, nach dem eine RCON-Verbindung getrennt wird. |
| `RCONUsePacketIdFix`           | bool   | Korrigiert Packet-IDs in Pocketpairs fehlerhafter RCON-Paketverarbeitung. |
| `logNetworking`                | bool   | Loggt eingehende Netzwerkdaten von Clients. |
| `logNetworkingToConsole`       | bool   | Loggt Netzwerkverkehr in die Konsole. |
| `logChat`                      | bool   | Loggt alle Chatnachrichten von Spielern. |
| `logRCON`                      | bool   | Loggt die Nutzung von RCON-Befehlen. |
| `logPlayerUID`                 | bool   | Loggt die PlayerUID in relevanten Logs. |
| `logPlayerIP`                  | bool   | Loggt die IP-Adresse von Spielern in relevanten Logs. |
| `logPlayerDeaths`              | bool   | Loggt Spielertode. |
| `logPlayerLogins`              | bool   | Loggt Logins und Logouts von Spielern. |
| `logPlayerBuildings`           | bool   | Loggt Bauaktionen von Spielern. (Bauen, Abbrechen, Demontieren) |
| `logHelicopterKills`           | bool   | Loggt Kills durch Helikopter. |
| `logPlayerSummons`             | bool   | Loggt Pal-Summons von Spielern. |
| `logPlayerCaptures`            | bool   | Loggt Pal-Fänge von Spielern. |
| `logCraftings`                 | bool   | Loggt Crafting-Aktionen von Spielern. |
| `logTechUnlocks`               | bool   | Loggt freigeschaltete Technologien von Spielern. |
| `logOpenOilrigBoxes`           | bool   | Loggt Interaktionen mit Oilrig-Kisten. |
| `OilrigGoalBoxLocktime`        | int    | Sekunden, die die Zielkiste im Oilrig gesperrt bleibt (Standard: `300`). |
| `useAdminWhitelist`            | bool   | Aktiviert die Admin-IP-Whitelist. **Die IPs müssen in `adminIPs` gesetzt werden!** |
| `adminAutoLogin`               | bool   | Loggt whitelisted Admins beim Beitritt automatisch in den Adminmodus ein. |
| `adminIPs`                     | array  | Liste von Admin-IPs, die Adminbefehle verwenden dürfen. |
| `bannedIPs`                    | array  | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter IP-Bann-Speicher. Nutze stattdessen `Banlist.json` und `/banip` oder `/unbanip`. |
| `bannedChatWords`              | array  | Chatfilter für blockierte Wörter (z. B. RMT-Werbung). |
| `bannedMessage`                | string | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alte Bannnachricht für Config-basierte Bannverarbeitung. |
| `bannedNames`                  | array  | Nicht erlaubte Spielernamen (z. B. aus gecrackten Versionen). |
| `pvpMaxToBuildingDamage`       | int    | Maximal erlaubter PvP-Schaden an Gebäuden. |
| `pvpMaxToPlayerDamage`         | int    | Maximal erlaubter PvP-Schaden an Spielern. |
| `pvpMaxToPalDamage`            | int    | Maximal erlaubter PvP-Schaden an Pals. |
| `pveMaxToPalBanThreshold`      | int    | PvE-Pal-Schadensgrenze, die Cheaterkennung auslöst. |
| `treeLimiter`                  | float  | Maximale Zeit, in der ein Spieler 1 Baum zerstören kann (z. B. `0.1` = 1 Baum alle 100 ms). Das verhindert starke Lags im Kampf, wenn Raketen schnell viele Bäume zerstören. |
| `allowAdminCheats`             | bool   | Erlaubt Admins die Nutzung von Cheat-Befehlen wie Godmode.                      |
| `allowGodmodeOnehit`           | bool   | Erlaubt Godmode, alles mit einem Treffer zu töten. |
| `adminCheats`                  | array  | Legt fest, welche Befehle als Admin-Cheats gelten. Wenn Admin-Cheats nicht erlaubt sind, können Admins sie nicht ausführen. RCON kann sie weiterhin ausführen. |
| `isChineseCmd`                 | bool   | Aktiviert chinesische Codierung in der Konsole (Legacy). |
| `announceConnections`          | bool   | Kündigt Spielerbeitritte und -abgänge im Chat an. |
| `dontAnnounceAdminConnections` | bool   | Unterdrückt Verbindungsnachrichten für Admins. |
| `announcePunishments`          | bool   | Kündigt Cheat-Banns/-Kicks allen Spielern im Chat an. |
| `announcePlayerDeaths`         | bool   | Zeigt öffentliche Todesmeldungen im Chat an. |
| `announceOpenOilrigBoxes`      | bool   | Kündigt Oilrig-Loot-Events im Chat an. |
| `announceHelicopterKills`      | bool   | Kündigt Helikopter-Kills im Chat an. |
| `announcePlayerSummons`        | bool   | Kündigt Pal-Summons von Spielern im Chat an. |
| `announceAdminSummons`         | bool   | Kündigt Pal-Summons durch Adminbefehle im Chat an. |
| `announceAdminSummonsKill`     | bool   | Kündigt an, wenn ein Spieler einen von einem Admin beschworenen Pal tötet. |
| `chatBypassWait`               | bool   | Entfernt die Chat-Abklingzeit zwischen Nachrichten.                                   |
| `chatMessageMaxLen`            | int    | Maximal erlaubte Länge von Chatnachrichten. |
| `useWhitelist`                 | bool   | Aktiviert `WhiteList.json`. |
| `whitelistMessage`             | string | Nachricht, die nicht gewhitelisteten Spielern angezeigt wird. |
| `steamidProtection`            | bool   | Verhindert doppelte Logins mit derselben UserId. |
| `blockTowerBossCapture`        | bool   | Deaktiviert das Fangen von Turmbossen. |
| `RCONbase64`                   | bool   | Aktiviert base64-codierte RCON-Befehle. |
| `disableIllegalItemProtection` | bool   | Deaktiviert den Schutz vor gemoddeten Items (z. B. Debug-Sphären). |
| `disableButchering`            | bool   | Deaktiviert das Schlachten. |
| `disableRenaming`              | bool   | Deaktiviert das Umbenennen von Charakteren. |
| `disablePalRenaming`           | bool   | Deaktiviert das Umbenennen von Pals. |
| `doActionUponIllegalPalStats`  | bool   | Reagiert automatisch auf illegale Pal-Stat-Exploits. |
| `palStatsMaxRank`              | int    | Maximal erlaubter Pal-Verstärkungsrang (`-1` = automatisch erkennen). |
| `bannedTechnologies`           | array  | Blockiert Technologien. Sie werden beim Beitritt verlernt. |
| `PalImport_Disabled`           | bool   | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alte Einstellung für die Migration von Pal-Importregeln. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_BanIfPalIsImpossible` | bool | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alte Einstellung für Strafen bei unmöglichen Pal-Importen. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_BannedPalIDs`       | array  | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alte Liste von Pal-IDs, die vom Import ausgeschlossen sind. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_AllowGenderNone`    | bool   | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alte Importregel für `Gender: "None"`. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxLevel`           | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Altes Maximallevel für Importe. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxRank`            | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter Maximalrang für Partner-Skills bei Importen. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxSoulHP`          | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter Maximalwert für Pal-Soul-Gesundheit. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxSoulATK`         | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter Maximalwert für Pal-Soul-Angriff. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxSoulDEF`         | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter Maximalwert für Pal-Soul-Verteidigung. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxSoulCS`          | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter Maximalwert für Pal-Soul-Handwerksgeschwindigkeit. Verwende stattdessen `Pals/ImportRules/Default.json`. |
| `PalImport_MaxIV`              | int    | <span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alter Maximalwert für IVs. Verwende stattdessen `Pals/ImportRules/Default.json`. |
