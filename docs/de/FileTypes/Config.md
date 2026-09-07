# 🛠️ `Config.json`

`Config.json` wird beim ersten Start in `<PalServer>/Pal/Binaries/Win64/PalDefender/` erzeugt. Stoppe den Server vor dem Bearbeiten oder führe nach dem Speichern `/reloadcfg` aus.

!!! note "Generierte Einstellungen"
    PalDefender schreibt den aktuellen Einstellungssatz in diese Datei zurück. Nicht aufgeführte Schlüssel sind veraltet, dienen nur der Migration oder sind im aktuellen öffentlichen Build nicht verfügbar.

## Allgemeines und Maßnahmen

| Schlüssel | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `version` | string | Aktuelle Version | Von PalDefender verwaltete Konfigurations-/Schemaversion. |
| `MOTD` | array | Drei Nachrichten | Nachrichten beim Beitritt. Unterstützt `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}` und `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | bool | `true` | Stoppt den Server, wenn PalDefender nicht initialisiert werden kann. Manche Hoster interpretieren dies als Absturz und starten wiederholt neu. |
| `preventAdminPasswordInChat` | bool | `true` | Verhindert, dass das Admin-Passwort als Chattext gesendet wird. |
| `shouldWarnCheaters` | bool | `true` | Warnt einen Spieler bei einer automatischen Erkennung. |
| `shouldWarnCheatersReason` | bool | `false` | Nimmt den Erkennungsgrund in diese Warnung auf. |
| `shouldKickCheaters` | bool | `true` | Kickt erkannte Cheater, sofern keine stärkere aktivierte Maßnahme greift. |
| `shouldBanCheaters` | bool | `false` | Bannt erkannte Cheater über ihr Konto. |
| `shouldIPBanCheaters` | bool | `false` | Bannt erkannte Cheater über ihre IP-Adresse. |
| `blockEmergencyRespawn` | bool | `true` | Blockiert Menü → Notfall-Respawn. |

## RCON und Logging

| Schlüssel | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` | Sekunden bis zum Timeout einer inaktiven RCON-Verbindung. |
| `RCONbase64` | bool | `false` | Aktiviert Base64-kodierte RCON-Befehle. |
| `logNetworking` | bool | `false` | Schreibt unterstützte Netzwerkprotokolle. Netzwerk-Logging ist im aktuellen öffentlichen Build deaktiviert. |
| `logNetworkingToConsole` | bool | `true` | Spiegelt Netzwerkprotokolle in die Konsole, sofern Netzwerk-Logging verfügbar ist. |
| `logChat` | bool | `true` | Protokolliert Global-, Gilden- und Say-Chat. |
| `logRCON` | bool | `false` | Protokolliert RCON-Befehle. |
| `logPlayerUID` | bool | `false` | Nimmt die PlayerUID in relevante Logs und AntiCheat-Webhooks auf. |
| `logPlayerIP` | bool | `true` | Nimmt IP-Adressen in relevante Logs und AntiCheat-Webhooks auf. |
| `logPlayerDeaths` | bool | `true` | Protokolliert Spielertode und Kills. |
| `logPlayerLogins` | bool | `true` | Protokolliert Beitritte und Verlassen. |
| `logPlayerBuildings` | bool | `true` | Protokolliert unterstützte Bau-, Abbruch-, Demontage- und Palbox-Verschiebeaktionen. |
| `logPlayerSummons` | bool | `true` | Protokolliert Raid-Boss-Beschwörungen durch Spieler. |
| `logPlayerCaptures` | bool | `true` | Reservierter Kompatibilitätsschlüssel. Capture-Logging ist in 1.9.0 wegen des unzuverlässigen Events deaktiviert. |
| `logPlayerDamage` | bool | `false` | Protokolliert von Spielern verursachte Damage-Events mit den gemeldeten Native-/Base-Damage-Werten in der Serverkonsole. Funktioniert unabhängig von der Damage-Cheat-Erkennung. |
| `BannedCampWorker` | array | Panthalus-Varianten | Character-IDs, die nicht an einer Basis eingesetzt werden dürfen. Der Vergleich ignoriert Groß-/Kleinschreibung; Varianten wie `BOSS_...` müssen separat aufgeführt werden. |
| `logHelicopterKills` | bool | `true` | Protokolliert Abschüsse des Kampfhubschraubers. |
| `logCraftings` | bool | `true` | Protokolliert Herstellung durch Spieler. |
| `logTechUnlocks` | bool | `true` | Protokolliert Technologie-Freischaltungen. |
| `logOpenOilrigBoxes` | bool | `true` | Protokolliert Ereignisse der Oil Rig End Goal Box. |
| `OilrigGoalBoxLocktime` | int | `300` | Sekunden, die die Oil Rig End Goal Box gesperrt bleibt. |

## Discord-Webhooks

`PalWebhooks` ist ein Objekt. Eine leere URL deaktiviert das jeweilige Ziel. Die Zustellung wird in eine Warteschlange gestellt, damit Nachrichtenspitzen zeitversetzt erfolgen und den Game-Thread nicht blockieren.

| Untergeordneter Schlüssel | Sendet |
| --- | --- |
| `webhookURL_Chat` | Global- und Say-Chatnachrichten. |
| `webhookURL_GuildChat` | Gildenchatnachrichten mit Gildennamen. |
| `webhookURL_Commands` | Im Spielchat ausgeführte Befehle einschließlich Administrator und vollständigem Befehl. |
| `webhookURL_Deaths` | Tode und Kills. Benötigt `announcePlayerDeaths` oder `logPlayerDeaths`. |
| `webhookURL_JoinLeave` | Beitritte/Verlassen, wenn `announceConnections` aktiv ist; beachtet `dontAnnounceAdminConnections`. |
| `webhookURL_Summons` | Spieler-/Admin-Summon-Ankündigungen und vollständige Schadensergebnisse verfolgter Summons. |
| `webhookURL_Oilrig` | Oil-Rig-Boxen und Hubschrauber-Kills, wenn die entsprechende `announce...`-Einstellung aktiv ist. |
| `webhookURL_AntiCheats` | Automatische und zur manuellen Prüfung bestimmte AntiCheat-Erkennungen. UID/IP folgen `logPlayerUID` und `logPlayerIP`. |

```json
"PalWebhooks": {
    "webhookURL_Chat": "",
    "webhookURL_GuildChat": "",
    "webhookURL_Commands": "",
    "webhookURL_Deaths": "",
    "webhookURL_JoinLeave": "",
    "webhookURL_Summons": "",
    "webhookURL_Oilrig": "",
    "webhookURL_AntiCheats": ""
}
```

## Administration, Chat und Ankündigungen

| Schlüssel | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` | Beschränkt Admin-Login/-Befehle auf `adminIPs`. |
| `adminAutoLogin` | bool | `false` | Aktiviert beim Beitritt automatisch den Admin-Modus für eine freigegebene IP. |
| `adminIPs` | array | `127.0.0.1` | Exakte IPs und unterstützte Wildcard-Einträge für die Serveradministration. |
| `bannedChatWords` | array | Häufige RMT-Begriffe | Chatfilter-Begriffe ohne Beachtung der Groß-/Kleinschreibung. |
| `bannedNames` | array | Bekannte Missbrauchsnamen | Beim Login abgelehnte Spielernamen. |
| `allowAdminCheats` | bool | `false` | Erlaubt Admins Befehle aus `adminCheats` und das Umgehen ausgewählter Schutzfunktionen. Die Admin-Waffe selbst benötigt nur aktiven Ingame-Adminstatus. |
| `allowGodmodeOnehit` | bool | `false` | Erlaubt Godmode-Nutzern One-Hit-Schaden. |
| `adminCheats` | array | Generierte Liste | Befehle, die bei deaktiviertem `allowAdminCheats` als Admin-Cheats gelten. RCON wird durch diese Liste nicht blockiert. |
| `announceConnections` | bool | `false` | Kündigt Beitritte/Verlassen im Chat an und aktiviert die Quelle für den Join/Leave-Webhook. |
| `dontAnnounceAdminConnections` | bool | `true` | Blendet Admin-Beitritte/-Abgänge aus diesen Ankündigungen aus. |
| `announcePunishments` | bool | `false` | Kündigt automatische Cheat-Kicks/-Banns an. |
| `announcePlayerDeaths` | bool | `false` | Kündigt Spielertode im Chat an. |
| `announceOpenOilrigBoxes` | bool | `false` | Kündigt Oil-Rig-Box-Ereignisse an und aktiviert ihre Webhook-Quelle. |
| `announceHelicopterKills` | bool | `false` | Kündigt Hubschrauber-Kills an und aktiviert ihre Webhook-Quelle. |
| `announcePlayerSummons` | bool | `false` | Kündigt Raid-Boss-Beschwörungen durch Spieler an. |
| `announceAdminSummons` | bool | `false` | Kündigt über Admin-Funktionen gespawnte Pals an. |
| `announceAdminSummonsKill` | bool | `true` | Kündigt Kills/Tode administrativ gespawnter Pals an. |
| `chatBypassWait` | bool | `true` | Entfernt die normale Wartezeit zwischen Chatnachrichten. |
| `chatMessageMaxLen` | int | `128` | Maximale akzeptierte Länge einer Chatnachricht. |
| `useWhitelist` | bool | `false` | Aktiviert `WhiteList.json`. |
| `whitelistMessage` | string | Generierter Text | Nachricht für einen abgelehnten, nicht freigegebenen Spieler. |
| `steamidProtection` | bool | `true` | Verhindert die gleichzeitige doppelte Nutzung einer UserId. |

## Gameplay-Validierung

| Schlüssel | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | int | `100` | Maximal erlaubter PvP-Schaden an Gebäuden. |
| `pvpMaxToPalDamage` | int | `1000` | Maximal erlaubter PvP-Schaden an Pals. |
| `pveMaxToPalBanThreshold` | int | `900000` | PvE-Pal-Schadensgrenze für die Cheat-Erkennung. |
| `droppedPalPickupRange` | int | `99999` | Maximal akzeptierte Distanz beim Aufheben eines fallengelassenen Pals. |
| `treeLimiter` | float | `0.1` | Mindestsekunden zwischen Baumzerstörungen zur Begrenzung großer Vegetationsereignisse. |
| `disableIllegalItemProtection` | bool | `false` | Deaktiviert den Schutz vor ungültigen/modifizierten Gegenständen. |
| `disableButchering` | bool | `false` | Blockiert das Schlachten von Pals. |
| `disableRenaming` | bool | `false` | Blockiert das Umbenennen von Spielern. |
| `disablePalRenaming` | bool | `false` | Blockiert das Umbenennen von Pals. |
| `doActionUponIllegalPalStats` | bool | `true` | Führt bei unmöglichen Pal-Werten die konfigurierte Cheat-Maßnahme aus. |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` | Blockiert Rezepte, die die angefragte Werkbank nicht unterstützt. |
| `preventDoctorSurgiExploit` | bool | `true` | Erkennt/blockiert den Doctor-Surgi-Exploit. |
| `doActionUponDoctorSurgiExploit` | bool | `true` | Führt für diesen Exploit die konfigurierte Cheat-Maßnahme aus. |
| `palStatsMaxRank` | int | `-1` | Maximaler Pal-Verstärkungsrang; `-1` verwendet automatische/aktuelle Spiellimits. |
| `bannedTechnologies` | array | Leer | Technologie-IDs, deren Lernen blockiert wird und die bei Erkennung entfernt werden. |

## AntiCheat-Funktionsschalter

| Schlüssel | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` | Kompatibilitätsschalter der alten AntiDupe-Funktion; im aktuellen Release-Build inaktiv. |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` | Altes Mindestintervall zwischen Bauaktionen; derzeit inaktiv. |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` | Altes Mindestintervall zwischen Demontagen; derzeit inaktiv. |
| `antiDupeShowBlockMessage` | bool | `true` | Alter Schalter für Blockiermeldungen; derzeit inaktiv. |
| `antiDupeBuildMessage` | string | Generierter Text | Alte Nachricht bei blockiertem Bauen; derzeit inaktiv. |
| `antiDupeDismantleMessage` | string | Generierter Text | Alte Nachricht bei blockierter Demontage; derzeit inaktiv. |
| `antiVacuumEnabled` | bool | `true` | Aktiviert den Schutz gegen Aufnahmen aus der Ferne. |
| `antiVacuumBlockAutoPickup` | bool | `true` | Wendet Anti-Vacuum auf normale automatische Aufnahmen an. |
| `antiVacuumBlockRelicObtain` | bool | `true` | Wendet die Prüfung auf Relikte an. |
| `antiVacuumBlockNoteObtain` | bool | `true` | Wendet die Prüfung auf Notizen an. |
| `antiVacuumBlockEggPickup` | bool | `true` | Wendet die Prüfung auf Eier an. |
| `antiVacuumMaxPickupDistance` | float | `800.0` | Maximal erlaubte Aufnahmedistanz für geschützte Anfragen. |
| `antiVacuumShowBlockMessage` | bool | `true` | Zeigt bei blockierter Aufnahme eine Nachricht an. |
| `antiVacuumBlockMessage` | string | Generierter Text | Nachricht bei blockierter Aufnahme aus der Ferne. |
| `staminaCheatDetectionEnabled` | bool | `true` | Aktiviert die Erkennung verdächtiger Stamina-Aktionen. |
| `baseCampDupeDetectionEnabled` | bool | `true` | Aktiviert die BaseCamp-Dupe-Erkennung. |
| `damageCheatDetectionEnabled` | bool | `true` | Aktiviert die Damage-Cheat-Erkennung. |
| `damageCheatDetectionTolerancePercent` | float | `5.0` | Zulässige prozentuale Abweichung zwischen gemeldetem Native Damage und dem rekonstruierten Wert `BasePower × AttackWithBuff`. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | float | `1.5` | Maximal zulässige Waffen-`BasePower` als Faktor des statischen `AttackValue` der ausgerüsteten Waffe. |
| `ammoCheatDetectionEnabled` | bool | `true` | Aktiviert die Erkennung manipulierter Munitions-/Waffenzustände. |

Die `antiDupe...`-Schlüssel werden zur Konfigurationskompatibilität weiterhin erzeugt, die alte AntiDupe-Funktion ist im aktuellen Release-Build jedoch deaktiviert. Verlasse dich nicht auf diese Optionen, bis die Funktion wieder aktiviert wird.

## Alte Migrationsschlüssel

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS` und `PalImport_MaxIV` werden nur gelesen, um ältere Installationen nach [`Pals/ImportRules/Default.json`](./PalImportRules.md) zu migrieren. Sie werden nicht mehr in aktuelle `Config.json`-Dateien geschrieben.

Die alten Schlüssel `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd` und `blockTowerBossCapture` gehören nicht mehr zur aktuellen Konfiguration. Banndaten werden in `Banlist.json` gespeichert.
