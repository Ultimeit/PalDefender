### [<<<](README.md) File Types

#### English / [简体中文](./Config_ZH_CN.md)

# Config.json

Explanation of every config entry:
|config name|values|description|
|-|-|-|
| `RCONbase64` | true, false | Set this to `true` to use base64 encoding in RCON. |
| `adminAutoLogin` | true, false | Auto login admins upon join. |
| `adminIPs` | `["127.0.0.1", "..."]` | IP addresses that are allowed to use admin commands. |
| `allowAdminCheats` | true, false | allows admins to use cheats. |
| `announceConnections` | true, false | Broadcast message when player joins/leaves server. |
| `announcePunishments` | true, false | Broadcast message when player gets kicked/banned by anticheat. |
| `bannedChatWords` | `["word1", "word2", "..."]` | Allows you to get rid of pesky RMT adverts. Messages containing words from this array will be blocked. |
| `bannedIPs` | `["127.0.0.1", "..."]` | List of banned IP addresses. |
| `bannedMessage` | "You are banned." | Allows you to customize message players see when they try to join your server while being IP banned. |
| `bannedNames` | `["anquan666", "Goldberg"]` | Some basic pirated versions protection. |
| `blockTowerBossCapture` | true, false | Enables/disables blocking of tower bosses capturing. |
| `chatBypassWait` | true, false | Allows you to get rid of 1 minute cooldown between sending chat messages. |
| `disableButchering` | true, false | It ain't perfect, but better than nothing if you want to fix dupe exploit with infinite butchering. |
| `disableIllegalItemProtection` | true, false | Disables protection against Debug/Robbery spheres (some mods add them as craftable items to the game). |
| `disablePalRenaming` | true, false | Disables Pal renamings. |
| `disableRenaming` | true, false | Disables renamings. |
| `doActionUponIllegalPalStats` | true, false | Allow automatic actions when a player tries to use an exploit to enhance pal stats more than allowed. |
| `isChineseCmd` | true, false | Set to true if the console should support Chinese encoding. Can be ignored on newer Windows versions. |
| `logChat` | true, false | Log all chat messages. |
| `logNetworking` | true, false | Log almost everything that players are sending to server. |
| `logPlayerIP` | true, false | Additionally logs the player IP whenever a log contains a player. |
| `logPlayerUID` | true, false | Additionally logs the player UniqueID whenever a log contains a player. |
| `logRCON` | true, false | Logs RCON commands. |
| `logPlayerDeaths` | true, false | When set to `false`, it will no longer log player deaths in the console. |
| `logPlayerLogins` | true, false | When set to `false`, it will no longer log player Logins and Logouts in the console. |
| `palStatsMaxRank` | any positive number including 0. | 0 deactivates pal enhancement completely. Any number above 0 sets a new limit. Default max rank is 20. So you can put 5 and it is limited to 5. -1 detects the server's max pal enhancement option, so default will be 10 but if a mod changes this number -1 will detect the mod's new limit. |
| `pveMaxToPalBanThreshold` | any positive number. | Attempting to deal damage to Pal higher than this number will flag player as cheater. |
| `pvpMaxToPalDamage` | any positive number. | Max damage that can be done to player owned pals **IF** pvp is enabled (bEnablePlayerToPlayerDamage). If damage exceeds this number, it will be floored down to it. Note: specifically this option is for damage before any damage mitigation. |
| `pvpMaxToBuildingDamage` | any positive number. | Same as `pvpMaxToPalDamage `, but against buildings. Note: specifically this option is for damage before any damage mitigation. |
| `shouldBanCheaters` | true, false | Allow cheat detection to ban cheaters. |
| `shouldIPBanCheaters` | true, false | Allow cheat detection to IP ban cheaters. |
| `shouldKickCheaters` | true, false | Allow cheat detection to kick cheaters. |
| `shouldWarnCheaters` | true, false | Warns cheaters in chat that they got caught. |
| `shouldWarnCheatersReason` | true, false | Provides them a reason why they got caught. |
| `steamidProtection` | true, false | Avoids that the same steamID can join the server while already logged in. |
| `useAdminWhitelist` | true, false | Enables/disables usage of admin IP whitelist system. |
| `useWhitelist` | true, false | Enables/disables SteamID whitelist. |
| `whitelistMessage` | "You are not whitelisted." | Allows you to customize the not whitelisted message. |
| `infiniteAmmoExploitActions` | true, false | When set to `false`, it will only log warnings in the console. |
| `infiniteAmmoExploitDisabled` | true, false | When set to `true`, it will ignore the feature completely. |
