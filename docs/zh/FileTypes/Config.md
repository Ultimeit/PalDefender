# 🛠️ Config.json

| 配置键                     | 类型   | 描述                                                               |
| ------------------------------ | ------ | ------------------------------------------------------------------------- |
| `version`                      | string | 配置版本标识符（例如 `"1.0.0"`）。                               |
| `MOTD`                         | array  | 每日消息。支持占位符：<br>`{ServerName}` -> 字符串 - 服务器名称<br>`{PlayerName}` -> 字符串 - 加入的玩家<br>`{Difficulty}` -> 字符串 - 如果在 palworld .ini 中设置<br>`{DeathPenalty}` -> 字符串<br>`{AllowGlobalPalboxExport}` -> "Enabled" / "Disabled"<br>`{AllowGlobalPalboxImport}` -> "Enabled" / "Disabled"<br>`{IsPvP}` -> "Enabled" / "Disabled"<br>`{IsHardcore}` -> "Enabled" / "Disabled"<br>`{FriendlyFire}` -> "Enabled" / "Disabled"<br>`{DayTimeSpeedRate}` -> 浮点数<br>`{NightTimeSpeedRate}` -> 浮点数<br>`{ExpRate}` -> 浮点数<br>`{PalCaptureRate}` -> 浮点数<br>`{PalSpawnNumRate}` -> 浮点数<br>`{PalEggDefaultHatchingTime}` -> 浮点数<br>`{EnemyDropItemRate}` -> 浮点数<br>`{PalStomachDecreaceRate}` -> 浮点数<br>`{PalStaminaDecreaceRate}` -> 浮点数<br>`{BaseCampMaxNumInGuild}` -> 整数<br>`{SupplyDropSpan}` -> 整数<br>`{MaxBuildingLimitNum}` -> 整数<br> |
| `exitServerOnStartupFailure`   | bool   | 如果为 `true`，当 PalDefender 无法启动时关闭服务器。有助于保护您的存档在没有 PalDefender 的情况下运行。**可能会导致某些不检查退出代码并假设游戏崩溃导致无限循环的服务器主机出现问题。**                   |
| `preventAdminPasswordInChat`   | bool   | 防止在聊天中泄露管理员密码。如果未设置管理员密码，则不起作用。                                |
| `shouldWarnCheaters`           | bool   | 在检测到作弊者时向他们发送警告消息。        |
| `shouldWarnCheatersReason`     | bool   | 在上面的作弊警告消息中包含原因。                   |
| `shouldKickCheaters`           | bool   | 自动踢出检测到的作弊者。                                    |
| `shouldBanCheaters`            | bool   | 自动封禁检测到的作弊者。                                     |
| `shouldIPBanCheaters`          | bool   | 自动 IP 封禁检测到的作弊者。                                  |
| `RCONTimeout`                  | float  | 允许您声明断开 RCON 连接的超时时间。                   |
| `RCONUsePacketIdFix`           | bool   | 修复 Pocketpair 错误实现的 RCON 数据包处理的包 ID。|
| `logNetworking`                | bool   | 记录来自客户端的传入网络数据。                                  |
| `logNetworkingToConsole`       | bool   | 将网络流量记录到控制台。                                      |
| `logChat`                      | bool   | 记录所有玩家聊天消息。                                            |
| `logRCON`                      | bool   | 记录 RCON 命令使用情况。                                                  |
| `logPlayerUID`                 | bool   | 在相关日志中记录玩家 PlayerUID。                                   |
| `logPlayerIP`                  | bool   | 在相关日志中记录玩家 IP 地址。                                  |
| `logPlayerDeaths`              | bool   | 记录玩家死亡。                                                       |
| `logPlayerLogins`              | bool   | 记录玩家登录/登出事件。                                          |
| `logPlayerBuildings`           | bool   | 记录玩家的建筑活动。（建造、取消、拆除）                  |
| `logHelicopterKills`           | bool   | 记录直升机击杀。                                                |
| `logPlayerSummons`             | bool   | 记录玩家帕鲁召唤。                                                  |
| `logPlayerCaptures`            | bool   | 记录玩家帕鲁捕获。                                                 |
| `logCraftings`                 | bool   | 记录玩家制作。                                                    |
| `logTechUnlocks`               | bool   | 记录玩家技术解锁。                                        |
| `logOpenOilrigBoxes`           | bool   | 记录石油钻井平台箱子交互。                                             |
| `OilrigGoalBoxLocktime`        | int    | 石油钻井平台目标箱子保持锁定状态的秒数（默认：`300`）。                |
| `useAdminWhitelist`            | bool   | 启用管理员 IP 白名单。**IP 必须在 `adminIPs` 中设置！**    |
| `adminAutoLogin`               | bool   | 加入时自动将白名单管理员登录到管理员模式。    |
| `adminIPs`                     | array  | 允许使用管理员命令的管理员 IP 列表。                          |
| `bannedIPs`                    | array  | 被阻止连接的 IP 列表。                                      |
| `bannedChatWords`              | array  | 聊天过滤器，用于阻止的词汇（例如，RMT 广告）。                            |
| `bannedMessage`                | string | 显示给被封禁玩家的消息。                                          |
| `bannedNames`                  | array  | 不允许的玩家名称（例如，来自破解版本）。                    |
| `pvpMaxToBuildingDamage`       | int    | 允许的最大 PvP 对建筑伤害。                                      |
| `pvpMaxToPalDamage`            | int    | 允许的最大 PvP 对帕鲁伤害。                                           |
| `pveMaxToPalBanThreshold`      | int    | 触发作弊检测的 PVE 帕鲁伤害阈值。                   |
| `treeLimiter`                  | float  | 玩家摧毁 1 棵树的最大时间（例如 `0.1` = 每 100 毫秒 1 棵树）。这可以避免在战斗中火箭快速杀死大量树木时出现巨大延迟。 |
| `allowAdminCheats`             | bool   | 允许管理员使用作弊命令，如无敌模式。                      |
| `allowGodmodeOnehit`           | bool   | 启用无敌模式一击必杀。                                      |
| `adminCheats`                  | array  | 允许您指定哪些命令被视为管理员作弊，因此如果不允许管理员作弊，您的管理员将无法执行这些命令。RCON 仍然可以执行这些命令。 |
| `isChineseCmd`                 | bool   | 在控制台中启用中文编码（遗留）。                             |
| `announceConnections`          | bool   | 在聊天中公告玩家加入/离开事件。                           |
| `dontAnnounceAdminConnections` | bool   | 抑制管理员的连接消息。                                |
| `announcePunishments`          | bool   | 在聊天中向所有玩家公告作弊封禁/踢出。                    |
| `announcePlayerDeaths`         | bool   | 在聊天中显示公开的死亡消息。                                  |
| `announceOpenOilrigBoxes`      | bool   | 在聊天中公告石油钻井平台战利品事件。                                 |
| `announceHelicopterKills`      | bool   | 在聊天中公告直升机击杀。                                   |
| `announcePlayerSummons`        | bool   | 在聊天中公告玩家帕鲁召唤。                             |
| `announceAdminSummons`         | bool   | 在聊天中公告管理员命令的帕鲁召唤。                      |
| `announceAdminSummonsKill`     | bool   | 当玩家杀死管理员召唤的帕鲁时公告。                 |
| `chatBypassWait`               | bool   | 移除消息之间的聊天冷却时间。                                   |
| `chatMessageMaxLen`            | int    | 允许的最大聊天消息长度。                                          |
| `useWhitelist`                 | bool   | 启用 `WhiteList.json`。                                                 |
| `whitelistMessage`             | string | 显示给非白名单玩家的消息。                                 |
| `steamidProtection`            | bool   | 防止使用相同 UserId 重复登录。                              |
| `blockTowerBossCapture`        | bool   | 禁用塔楼 Boss 捕获。                                         |
| `RCONbase64`                   | bool   | 启用 base64 编码的 RCON 命令。                                     |
| `disableIllegalItemProtection` | bool   | 禁用对修改物品的保护（例如，调试球）。           |
| `disableButchering`            | bool   | 禁用屠宰。                                                      |
| `disableRenaming`              | bool   | 禁用角色重命名。                                              |
| `disablePalRenaming`           | bool   | 禁用帕鲁重命名。                                                |
| `doActionUponIllegalPalStats`  | bool   | 自动对非法帕鲁属性漏洞利用做出反应。                        |
| `palStatsMaxRank`              | int    | 允许的最大帕鲁强化等级（`-1` = 自动检测）。                    |
| `bannedTechnologies`           | array  | 阻止学习技术。加入时取消学习。        |
