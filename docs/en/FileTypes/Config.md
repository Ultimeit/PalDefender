# 🛠️ Config.json

| Config Key                     | Type   | Description                                                               |
| ------------------------------ | ------ | ------------------------------------------------------------------------- |
| `version`                      | string | Config version identifier (e.g. `"1.0.0"`).                               |
| `MOTD`                         | array  | Message of the Day. Supports placeholders:<br>`{ServerName}` -> String - name of the server<br>`{PlayerName}` -> String - player who joined<br>`{Difficulty}` -> String - if set in palworld .ini<br>`{DeathPenalty}` -> String<br>`{AllowGlobalPalboxExport}` -> "Enabled" / "Disabled"<br>`{AllowGlobalPalboxImport}` -> "Enabled" / "Disabled"<br>`{IsPvP}` -> "Enabled" / "Disabled"<br>`{IsHardcore}` -> "Enabled" / "Disabled"<br>`{FriendlyFire}` -> "Enabled" / "Disabled"<br>`{DayTimeSpeedRate}` -> Float number<br>`{NightTimeSpeedRate}` -> Float number<br>`{ExpRate}` -> Float number<br>`{PalCaptureRate}` -> Float number<br>`{PalSpawnNumRate}` -> Float number<br>`{PalEggDefaultHatchingTime}` -> Float number<br>`{EnemyDropItemRate}` -> Float number<br>`{PalStomachDecreaceRate}` -> Float number<br>`{PalStaminaDecreaceRate}` -> Float number<br>`{BaseCampMaxNumInGuild}` -> Int number<br>`{SupplyDropSpan}` -> Int number<br>`{MaxBuildingLimitNum}` -> Int number<br> |
| `exitServerOnStartupFailure`   | bool   | If `true`, shuts down the server when PalDefender cannot start. Good to protect your savegame being run without PalDefender. **Might cause problems with some Server Hosts, that do not check Exit Codes and assume the game crashed causing an endless loop.**                   |
| `preventAdminPasswordInChat`   | bool   | Prevents leaking admin passwords in chat. Does nothing if no admin password is set.                                |
| `shouldWarnCheaters`           | bool   | Sends a warning message to detected cheaters when they got caught.        |
| `shouldWarnCheatersReason`     | bool   | Includes the reason in the cheat warning message above.                   |
| `shouldKickCheaters`           | bool   | Automatically kicks detected cheaters.                                    |
| `shouldBanCheaters`            | bool   | Automatically bans detected cheaters.                                     |
| `shouldIPBanCheaters`          | bool   | Automatically IP-bans detected cheaters.                                  |
| `RCONTimeout`                  | float  | Lets you declare the timeout to drop a RCON connection.                   |
| `RCONUsePacketIdFix`           | bool   | Fixes packet IDs of pocketpairs wrong implemented of ROCN packet handling.|
| `logNetworking`                | bool   | Logs incoming network data from clients.                                  |
| `logNetworkingToConsole`       | bool   | Logs network traffic to the console.                                      |
| `logChat`                      | bool   | Logs all player chat messages.                                            |
| `logRCON`                      | bool   | Logs RCON command usage.                                                  |
| `logPlayerUID`                 | bool   | Logs player PlayerUID in relevant logs.                                   |
| `logPlayerIP`                  | bool   | Logs player IP address in relevant logs.                                  |
| `logPlayerDeaths`              | bool   | Logs player deaths.                                                       |
| `logPlayerLogins`              | bool   | Logs player login/logout events.                                          |
| `logPlayerBuildings`           | bool   | Logs construction by players.                                             |
| `logHelicopterKills`           | bool   | Logs kills by helicopters.                                                |
| `logPlayerSummons`             | bool   | Logs player Pal summons.                                                  |
| `logCraftings`                 | bool   | Logs player craftings.                                                    |
| `logTechUnlocks`               | bool   | Logs player technology unlockings.                                        |
| `logOpenOilrigBoxes`           | bool   | Logs oilrig box interactions.                                             |
| `OilrigGoalBoxLocktime`        | int    | Seconds the oilrig goal box stays locked (default: `300`).                |
| `useAdminWhitelist`            | bool   | Enables admin IP whitelist. **The IPs have to bet set in `adminIPs`!**    |
| `adminAutoLogin`               | bool   | Automatically logs in whitelisted admins into admin mode when joining.    |
| `adminIPs`                     | array  | List of admin IPs allowed to use admin commands.                          |
| `bannedIPs`                    | array  | List of IPs blocked from connecting.                                      |
| `bannedChatWords`              | array  | Chat filter for blocked words (e.g., RMT ads).                            |
| `bannedMessage`                | string | Message shown to banned players.                                          |
| `bannedNames`                  | array  | Disallowed player names (e.g., from cracked versions).                    |
| `pvpMaxToBuildingDamage`       | int    | Max allowed PvP damage to buildings.                                      |
| `pvpMaxToPalDamage`            | int    | Max allowed PvP damage to Pals.                                           |
| `pveMaxToPalBanThreshold`      | int    | PVE Pal damage threshold that triggers cheat detection.                   |
| `treeLimiter`                  | float  | Max time a player can destroy 1 tree. (e.g. `0.1` = 1 tree every 100ms). This avoids huge lag during combat where rockets kill plenty of trees quickly. |
| `allowAdminCheats`             | bool   | Allows admins to use cheat commands such as godmode.                      |
| `allowGodmodeOnehit`           | bool   | Enables godmode to one-hit anything.                                      |
| `adminCheats`                  | array  | Lets you specify which command is considered as an admin cheat, so if admin cheats are not allowed, they cannot be executed by your admins. RCON can still execute those. |
| `isChineseCmd`                 | bool   | Enables Chinese encoding in console (legacy).                             |
| `announceConnections`          | bool   | Announces player join/leave events in the chat.                           |
| `dontAnnounceAdminConnections` | bool   | Suppresses connection messages for admins.                                |
| `announcePunishments`          | bool   | Announces cheat bans/kicks to all players in the chat.                    |
| `announcePlayerDeaths`         | bool   | Shows public death messages in the chat.                                  |
| `announceOpenOilrigBoxes`      | bool   | Announces oilrig loot events in the chat.                                 |
| `announceHelicopterKills`      | bool   | Announces helicopter kills in the chat.                                   |
| `announcePlayerSummons`        | bool   | Announces Pal summons by players in the chat.                             |
| `announceAdminSummons`         | bool   | Announces Pal summons by admin commands in the chat.                      |
| `announceAdminSummonsKill`     | bool   | Announces when a player kills a summoned pal by an admin.                 |
| `chatBypassWait`               | bool   | Removes chat cooldown between messages.                                   |
| `chatMessageMaxLen`            | int    | Max allowed chat message length.                                          |
| `useWhitelist`                 | bool   | Enables `WhiteList.json`.                                                 |
| `whitelistMessage`             | string | Message shown to non-whitelisted players.                                 |
| `steamidProtection`            | bool   | Prevents duplicate logins using same UserId.                              |
| `blockTowerBossCapture`        | bool   | Disables capture of tower bosses.                                         |
| `RCONbase64`                   | bool   | Enables base64-encoded RCON commands.                                     |
| `disableIllegalItemProtection` | bool   | Disables protection against modded items (e.g., debug spheres).           |
| `disableButchering`            | bool   | Disables butchering.                                                      |
| `disableRenaming`              | bool   | Disables character renaming.                                              |
| `disablePalRenaming`           | bool   | Disables renaming of Pals.                                                |
| `doActionUponIllegalPalStats`  | bool   | Automatically reacts to illegal Pal stat exploits.                        |
| `palStatsMaxRank`              | int    | Max allowed Pal enhancement rank (`-1` = auto-detect).                    |
| `bannedTechnologies`           | array  | Blocks technologies from being learnt. Unlearns them upon joining.        |
