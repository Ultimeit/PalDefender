# 🛠️ `Config.json`

`Config.json` is generated in `<PalServer>/Pal/Binaries/Win64/PalDefender/` on first start. Stop the server before editing it, or use `/reloadcfg` after saving changes.

!!! note "Generated settings"
    PalDefender writes the current setting set back to this file. Keys not listed below are obsolete, migration-only, or unavailable in the current public build.

## General and enforcement

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `version` | string | Current version | Config schema/version marker maintained by PalDefender. |
| `MOTD` | array | Three messages | Join messages. Supports `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}`, and `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | bool | `true` | Stops the server if PalDefender cannot initialize. Some hosts may interpret this as a crash and restart repeatedly. |
| `preventAdminPasswordInChat` | bool | `true` | Blocks the admin password from being sent as chat text. |
| `shouldWarnCheaters` | bool | `true` | Warns a player when an automatic detection triggers. |
| `shouldWarnCheatersReason` | bool | `false` | Includes the detection reason in that warning. |
| `shouldKickCheaters` | bool | `true` | Kicks detected cheaters unless a stronger enabled action applies. |
| `shouldBanCheaters` | bool | `false` | Account-bans detected cheaters. |
| `shouldIPBanCheaters` | bool | `false` | IP-bans detected cheaters. |
| `blockEmergencyRespawn` | bool | `true` | Blocks the Menu → Emergency Respawn action. |

## RCON and logging

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` | Seconds before an inactive RCON connection times out. |
| `RCONbase64` | bool | `false` | Enables base64-encoded RCON commands. |
| `logNetworking` | bool | `false` | Writes supported network logging. Network logging is disabled in the current public build. |
| `logNetworkingToConsole` | bool | `true` | Mirrors network logging to the console when network logging is available. |
| `logChat` | bool | `true` | Logs Global, Guild, and Say chat. |
| `logRCON` | bool | `false` | Logs RCON commands. |
| `logPlayerUID` | bool | `false` | Includes PlayerUID in relevant logs and anti-cheat webhooks. |
| `logPlayerIP` | bool | `true` | Includes IP addresses in relevant logs and anti-cheat webhooks. |
| `logPlayerDeaths` | bool | `true` | Logs player deaths and kills. |
| `logPlayerLogins` | bool | `true` | Logs player joins and leaves. |
| `logPlayerBuildings` | bool | `true` | Logs supported build, cancellation, dismantle, and Palbox-move activity. |
| `logPlayerSummons` | bool | `true` | Logs player raid-boss summons. |
| `logPlayerCaptures` | bool | `true` | Reserved compatibility setting. Capture logging is disabled in 1.9.0 because the available event is unreliable. |
| `logPlayerDamage` | bool | `false` | Logs player-originated damage events and their reported native/base damage values to the server console. Works independently of damage cheat detection. |
| `BannedCampWorker` | array | Panthalus variants | Character IDs that cannot be assigned at a base. Matching is case-insensitive; variants such as `BOSS_...` must be listed separately. |
| `logHelicopterKills` | bool | `true` | Logs combat-helicopter kills. |
| `logCraftings` | bool | `true` | Logs player crafting. |
| `logTechUnlocks` | bool | `true` | Logs technology unlocks. |
| `logOpenOilrigBoxes` | bool | `true` | Logs Oil Rig End Goal Box events. |
| `OilrigGoalBoxLocktime` | int | `300` | Seconds the Oil Rig End Goal Box remains locked. |

## Discord webhooks

`PalWebhooks` is an object. Leave an individual URL empty to disable that destination. Webhook delivery is queued, so bursts are staggered instead of blocking the game thread.

| Nested key | Sends |
| --- | --- |
| `webhookURL_Chat` | Global and Say chat messages. |
| `webhookURL_GuildChat` | Guild chat messages with the guild name. |
| `webhookURL_Commands` | Commands run through in-game chat, including the administrator and full command. |
| `webhookURL_Deaths` | Deaths and kills. Requires `announcePlayerDeaths` or `logPlayerDeaths`. |
| `webhookURL_JoinLeave` | Join/leave events when `announceConnections` is enabled; respects `dontAnnounceAdminConnections`. |
| `webhookURL_Summons` | Player/admin summon announcements and complete tracked-summon damage results. |
| `webhookURL_Oilrig` | Oil Rig boxes and helicopter kills when the corresponding `announce...` setting is enabled. |
| `webhookURL_AntiCheats` | Automatic and manual-review anti-cheat detections. UID/IP inclusion follows `logPlayerUID` and `logPlayerIP`. |

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

## Administration, chat, and announcements

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` | Restricts admin login/commands to `adminIPs`. |
| `adminAutoLogin` | bool | `false` | Automatically enables admin mode for a joining whitelisted IP. |
| `adminIPs` | array | `127.0.0.1` | Exact IPs and supported wildcard entries allowed to administer the server. |
| `bannedChatWords` | array | Common RMT terms | Case-insensitive chat filter terms. |
| `bannedNames` | array | Known abuse names | Player names rejected during login. |
| `allowAdminCheats` | bool | `false` | Allows administrators to use commands in `adminCheats` and bypass selected protections. The Admin Gun itself only requires active in-game administrator status. |
| `allowGodmodeOnehit` | bool | `false` | Allows Godmode users to deal one-hit damage. |
| `adminCheats` | array | Generated list | Commands treated as admin cheats when `allowAdminCheats` is disabled. RCON is not blocked by this list. |
| `announceConnections` | bool | `false` | Announces joins/leaves in chat and enables the join/leave webhook source. |
| `dontAnnounceAdminConnections` | bool | `true` | Hides administrator joins/leaves from those announcements. |
| `announcePunishments` | bool | `false` | Announces automatic cheat kicks/bans. |
| `announcePlayerDeaths` | bool | `false` | Announces player deaths in chat. |
| `announceOpenOilrigBoxes` | bool | `false` | Announces Oil Rig box events and enables their webhook source. |
| `announceHelicopterKills` | bool | `false` | Announces helicopter kills and enables their webhook source. |
| `announcePlayerSummons` | bool | `false` | Announces player raid-boss summons. |
| `announceAdminSummons` | bool | `false` | Announces Pals spawned through administrative summon features. |
| `announceAdminSummonsKill` | bool | `true` | Announces kills/deaths of administratively summoned Pals. |
| `chatBypassWait` | bool | `true` | Removes the normal chat wait between messages. |
| `chatMessageMaxLen` | int | `128` | Maximum accepted chat-message length. |
| `useWhitelist` | bool | `false` | Enables `WhiteList.json`. |
| `whitelistMessage` | string | Generated text | Message shown to a rejected non-whitelisted player. |
| `steamidProtection` | bool | `true` | Rejects duplicate simultaneous use of a UserId. |

## Gameplay validation

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | int | `100` | Maximum permitted PvP damage to buildings. |
| `pvpMaxToPalDamage` | int | `1000` | Maximum permitted PvP damage to Pals. |
| `pveMaxToPalBanThreshold` | int | `900000` | PvE Pal-damage threshold used by cheat detection. |
| `droppedPalPickupRange` | int | `99999` | Maximum accepted distance for a dropped-Pal pickup. |
| `treeLimiter` | float | `0.1` | Minimum seconds between tree destruction events used to limit foliage bursts. |
| `disableIllegalItemProtection` | bool | `false` | Disables invalid/modded item protection. |
| `disableButchering` | bool | `false` | Blocks Pal butchering. |
| `disableRenaming` | bool | `false` | Blocks player renaming. |
| `disablePalRenaming` | bool | `false` | Blocks Pal renaming. |
| `doActionUponIllegalPalStats` | bool | `true` | Applies the configured cheat action for impossible Pal stats. |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` | Blocks recipes unsupported by the requested workbench. |
| `preventDoctorSurgiExploit` | bool | `true` | Detects/blocks the Doctor Surgi exploit. |
| `doActionUponDoctorSurgiExploit` | bool | `true` | Applies the configured cheat action for that exploit. |
| `palStatsMaxRank` | int | `-1` | Maximum Pal enhancement rank; `-1` uses automatic/current game limits. |
| `bannedTechnologies` | array | Empty | Technology IDs blocked from learning and removed when detected. |

## Anti-cheat feature switches

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` | Compatibility switch for the legacy AntiDupe feature; inactive in the current release build. |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` | Legacy minimum interval between builds; currently inactive. |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` | Legacy minimum interval between dismantles; currently inactive. |
| `antiDupeShowBlockMessage` | bool | `true` | Legacy block-message switch; currently inactive. |
| `antiDupeBuildMessage` | string | Generated text | Legacy build-block message; currently inactive. |
| `antiDupeDismantleMessage` | string | Generated text | Legacy dismantle-block message; currently inactive. |
| `antiVacuumEnabled` | bool | `true` | Enables remote pickup (vacuum) protection. |
| `antiVacuumBlockAutoPickup` | bool | `true` | Applies anti-vacuum checks to normal auto-pickups. |
| `antiVacuumBlockRelicObtain` | bool | `true` | Applies checks to relic collection. |
| `antiVacuumBlockNoteObtain` | bool | `true` | Applies checks to note collection. |
| `antiVacuumBlockEggPickup` | bool | `true` | Applies checks to egg pickup. |
| `antiVacuumMaxPickupDistance` | float | `800.0` | Maximum permitted pickup distance for protected requests. |
| `antiVacuumShowBlockMessage` | bool | `true` | Shows a player-facing message when a pickup is blocked. |
| `antiVacuumBlockMessage` | string | Generated text | Message shown for a blocked remote pickup. |
| `staminaCheatDetectionEnabled` | bool | `true` | Enables suspicious stamina-action detection. |
| `baseCampDupeDetectionEnabled` | bool | `true` | Enables base-camp duplication detection. |
| `damageCheatDetectionEnabled` | bool | `true` | Enables damage cheat detection. |
| `damageCheatDetectionTolerancePercent` | float | `5.0` | Permitted percentage difference between reported native damage and the reconstructed `BasePower × AttackWithBuff` value. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | float | `1.5` | Maximum permitted weapon `BasePower` as a multiplier of the equipped weapon's static `AttackValue`. |
| `ammoCheatDetectionEnabled` | bool | `true` | Enables ammunition/weapon-state cheat detection. |

The `antiDupe...` keys are still generated for configuration compatibility, but the legacy AntiDupe feature is disabled in the current release build. Do not rely on these controls until the feature is enabled again.

## Legacy migration keys

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS`, and `PalImport_MaxIV` are read only to migrate older installations to [`Pals/ImportRules/Default.json`](./PalImportRules.md). They are no longer written to current `Config.json` files.

The old `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd`, and `blockTowerBossCapture` keys are not part of the current configuration. Ban records belong in `Banlist.json`.
