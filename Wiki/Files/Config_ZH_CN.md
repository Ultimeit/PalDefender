### [<<<](README_ZH_CN.md) 文件类型

#### [English](./Config.md) / 简体中文

# Config.json

以下是每个配置项的的说明:
| 配置项 | 值 | 说明 |
|--------|-----|------|
| `RCONbase64` | true, false | 设置为`true`可以在RCON中使用Base64编码 优点：适用于unicode字符（中文/韩语/俄语/等）缺点： 您只能使用支持编码/解码 base64的RCON客户端。 |
| `adminAutoLogin` | true, false | 如果您的IP与管理员白名单匹配，则自动授予您管理员权限。 |
| `adminIPs` | `["127.0.0.1", "..."]` | 允许使用管理员指令的白名单IP地址列表。 |
| `allowAdminCheats` | true, false | 允许管理员进行作弊行为而不会受到惩罚。 |
| `announceConnections` | true, false | 当玩家加入/离开服务器时广播消息。 |
| `announcePunishments` | true, false | 当玩家被反作弊系统踢出或封禁时广播消息。 |
| `bannedChatWords` | `["word1", "word2", "..."]` | 用于过滤RMT（即现实金钱交易，用现实货币交易虚拟物品的行为）广告的单词列表。包含这些词的消息将被阻止。 |
| `bannedIPs` | `["127.0.0.1", "..."]` | 被封禁的IP地址列表。 |
| `bannedMessage` | "You are banned." | 允许您自定义玩家在 IP 被禁止时尝试加入您的服务器时看到的消息（支持中文）。 |
| `bannedNames` | `["anquan666", "Goldberg"]` | 一些基本的盗版保护（封禁的玩家昵称）。 |
| `blockTowerBossCapture` | true, false | 启用/禁用捕捉高塔boss。 |
| `chatBypassWait` | true, false | 可以让你在发送聊天信息时不再有1分钟的冷却时间。 |
| `disableButchering` | true, false | 禁用屠宰功能，以防止无限屠宰的物品复制漏洞。 |
| `disableIllegalItemProtection` | true, false | 禁用对调试/抢劫球体（某些模组将其作为可制作物品添加到游戏中）的保护。 |
| `disablePalRenaming` | true, false | Disables Pal renamings. |
| `disableRenaming` | true, false | 禁用玩家重命名功能（他们仍然可以改宠物的名字）。 |
| `doActionUponIllegalPalStats` | true, false | 检测到作弊时执行操作（设置为 false，则在检测到作弊时不会执行踢出或封禁等操作，需要人工判断）。 |
| `isChineseCmd` | true, false | 如果你希望显示中文字符并使用默认的windows命令行，请将此设置为`true`。在较新的Windows版本中可以忽略。 |
| `logChat` | true, false | 将所有聊天消息记录到日志。 |
| `logNetworking` | true, false | 将玩家发送给服务器的几乎所有网络数据记录到日志。 |
| `logPlayerIP` | true, false | Additionally logs the player IP whenever a log contains a player. |
| `logPlayerUID` | true, false | Additionally logs the player UniqueID whenever a log contains a player. |
| `logRCON` | true, false | 将所有RCON命令记录到日志。 |
| `logPlayerDeaths` | true, false | When set to `false`, it will no longer log player deaths in the console. |
| `logPlayerLogins` | true, false | When set to `false`, it will no longer log player Logins and Logouts in the console. |
| `palStatsMaxRank` | 任何正数（包括0） | 设置强化帕鲁的最大等级限制。设置为0任何玩家都无法强化帕鲁。任何大于0的数值将设置新的限制，默认为10。如果设置为-1，将检测服务器的最大帕鲁强化等级，并相应地更新此值。 |
| `pveMaxToPalBanThreshold` | 任何正数 | 尝试对高于此数值的帕鲁造成伤害时，将标记为作弊者。 |
| `pvpMaxToPalDamage` | 任何正数 | 如果启用PVP（bEnablePlayerToPlayerDamage），玩家对帕鲁造成的最大伤害超过此数值，将会被限制为该数值。此选项适用于未经任何伤害减免的伤害。 |
| `pvpMaxToBuildingDamage` | 任何正数 | 同`pvpMaxToPalDamage`，但针对建筑物。此选项适用于未经任何伤害减免的伤害。 |
| `shouldBanCheaters` | true, false | 允许反作弊系统自动封禁作弊者。 |
| `shouldIPBanCheaters` | true, false | 允许反作弊系统自动封禁作弊者IP。 |
| `shouldKickCheaters` | true, false | 允许反作弊系统自动踢出作弊者。 |
| `shouldWarnCheaters` | true, false | 允许反作弊系统在聊天中警告作弊者。 |
| `shouldWarnCheatersReason` | true, false | 提供作弊者被警告的原因。 |
| `steamidProtection` | true, false | 防止相同的SteamID在玩家已经登录时再次加入服务器。 |
| `useAdminWhitelist` | true, false | 启用/禁用管理员IP白名单系统（仅有adminIPs中的IP地址的玩家可以通过/adminpassword指令获得管理员权限）。 |
| `useWhitelist` | true, false | 启用/禁用SteamID白名单（仅有在SteamID白名单列表中的玩家可以进入服务器）。 |
| `whitelistMessage` | "You are not whitelisted." | 自定义未被列入白名单时显示的消息（支持中文）。 |
| `infiniteAmmoExploitActions` | true, false | When set to `false`, it will only log warnings in the console. |
| `infiniteAmmoExploitDisabled` | true, false | When set to `true`, it will ignore the feature completely. |
