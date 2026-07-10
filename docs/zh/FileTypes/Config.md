# 🛠️ Config.json

| 配置键                     | 类型   | 描述                                                               |
| ------------------------------ | ------ | ------------------------------------------------------------------------- |
| `version`                      | string | 配置版本标识（例如 `"1.0.0"`）。 |
| `MOTD`                         | array  | 每日消息。支持占位符：<br>`{ServerName}` -> String - 服务器名称<br>`{PlayerName}` -> String - 加入的玩家<br>`{Difficulty}` -> String - 如果已在 Palworld .ini 中设置<br>`{DeathPenalty}` -> String<br>`{AllowGlobalPalboxExport}` -> "Enabled" / "Disabled"<br>`{AllowGlobalPalboxImport}` -> "Enabled" / "Disabled"<br>`{IsPvP}` -> "Enabled" / "Disabled"<br>`{IsHardcore}` -> "Enabled" / "Disabled"<br>`{FriendlyFire}` -> "Enabled" / "Disabled"<br>`{DayTimeSpeedRate}` -> 浮点数<br>`{NightTimeSpeedRate}` -> 浮点数<br>`{ExpRate}` -> 浮点数<br>`{PalCaptureRate}` -> 浮点数<br>`{PalSpawnNumRate}` -> 浮点数<br>`{PalEggDefaultHatchingTime}` -> 浮点数<br>`{EnemyDropItemRate}` -> 浮点数<br>`{PalStomachDecreaceRate}` -> 浮点数<br>`{PalStaminaDecreaceRate}` -> 浮点数<br>`{BaseCampMaxNumInGuild}` -> 整数<br>`{SupplyDropSpan}` -> 整数<br>`{MaxBuildingLimitNum}` -> 整数<br> |
| `exitServerOnStartupFailure`   | bool   | 如果为 `true`，PalDefender 无法启动时会关闭服务器。这有助于避免存档在没有 PalDefender 的情况下运行。**某些服务器主机不检查退出码，可能会误认为游戏崩溃并进入无限重启循环。** |
| `preventAdminPasswordInChat`   | bool   | 防止管理员密码泄露到聊天中。如果未设置管理员密码，则没有效果。 |
| `shouldWarnCheaters`           | bool   | 检测到作弊者时向其发送警告消息。        |
| `shouldWarnCheatersReason`     | bool   | 在上述作弊警告消息中包含原因。 |
| `shouldKickCheaters`           | bool   | 自动踢出检测到的作弊者。 |
| `shouldBanCheaters`            | bool   | 自动封禁检测到的作弊者。 |
| `shouldIPBanCheaters`          | bool   | 自动对检测到的作弊者执行 IP 封禁。 |
| `RCONTimeout`                  | float  | RCON 连接超时后断开的时间。 |
| `RCONUsePacketIdFix`           | bool   | 修复 Pocketpair RCON 数据包处理中错误实现的 packet ID。 |
| `logNetworking`                | bool   | 记录来自客户端的传入网络数据。 |
| `logNetworkingToConsole`       | bool   | 将网络流量记录到控制台。 |
| `logChat`                      | bool   | 记录所有玩家聊天消息。 |
| `logRCON`                      | bool   | 记录 RCON 命令使用情况。 |
| `logPlayerUID`                 | bool   | 在相关日志中记录玩家 PlayerUID。 |
| `logPlayerIP`                  | bool   | 在相关日志中记录玩家 IP 地址。 |
| `logPlayerDeaths`              | bool   | 记录玩家死亡。 |
| `logPlayerLogins`              | bool   | 记录玩家登录/登出事件。 |
| `logPlayerBuildings`           | bool   | 记录玩家建筑操作。（建造、取消、拆除） |
| `logHelicopterKills`           | bool   | 记录直升机击杀。 |
| `logPlayerSummons`             | bool   | 记录玩家 Pal 召唤。 |
| `logPlayerCaptures`            | bool   | 记录玩家捕获 Pal。 |
| `logCraftings`                 | bool   | 记录玩家制作行为。 |
| `logTechUnlocks`               | bool   | 记录玩家科技解锁。 |
| `logOpenOilrigBoxes`           | bool   | 记录油田箱子交互。 |
| `OilrigGoalBoxLocktime`        | int    | 油田目标箱保持锁定的秒数（默认：`300`）。 |
| `useAdminWhitelist`            | bool   | 启用管理员 IP 白名单。**IP 必须设置在 `adminIPs` 中！**    |
| `adminAutoLogin`               | bool   | 白名单管理员加入时自动进入管理员模式。 |
| `adminIPs`                     | array  | 允许使用管理员命令的管理员 IP 列表。 |
| `bannedIPs`                    | array  | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版 IP 封禁存储。请改用 `Banlist.json` 以及 `/banip` 或 `/unbanip`。 |
| `bannedChatWords`              | array  | 被屏蔽词语的聊天过滤器（例如 RMT 广告）。 |
| `bannedMessage`                | string | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版基于 Config 的封禁消息设置。 |
| `bannedNames`                  | array  | 不允许使用的玩家名称（例如来自破解版本的名称）。 |
| `pvpMaxToBuildingDamage`       | int    | 允许的最大 PvP 建筑伤害。 |
| `pvpMaxToPalDamage`            | int    | 允许的最大 PvP Pal 伤害。 |
| `pveMaxToPalBanThreshold`      | int    | 触发作弊检测的 PvE Pal 伤害阈值。 |
| `treeLimiter`                  | float  | 玩家摧毁 1 棵树的最短间隔（例如 `0.1` = 每 100ms 1 棵树）。这可避免战斗中火箭快速摧毁大量树木造成严重卡顿。 |
| `allowAdminCheats`             | bool   | 允许管理员使用 godmode 等作弊命令。                      |
| `allowGodmodeOnehit`           | bool   | 允许 godmode 一击击杀任何目标。 |
| `adminCheats`                  | array  | 指定哪些命令被视为管理员作弊命令。如果不允许管理员作弊，管理员无法执行这些命令；RCON 仍可执行。 |
| `isChineseCmd`                 | bool   | 启用控制台中文编码（旧版）。 |
| `announceConnections`          | bool   | 在聊天中公告玩家加入/离开事件。 |
| `dontAnnounceAdminConnections` | bool   | 隐藏管理员的连接消息。 |
| `announcePunishments`          | bool   | 在聊天中向所有玩家公告作弊封禁/踢出。 |
| `announcePlayerDeaths`         | bool   | 在聊天中显示公开死亡消息。                                  |
| `announceOpenOilrigBoxes`      | bool   | 在聊天中公告油田战利品事件。 |
| `announceHelicopterKills`      | bool   | 在聊天中公告直升机击杀。 |
| `announcePlayerSummons`        | bool   | 在聊天中公告玩家召唤 Pal。 |
| `announceAdminSummons`         | bool   | 在聊天中公告管理员命令召唤 Pal。 |
| `announceAdminSummonsKill`     | bool   | 当玩家击杀由管理员召唤的 Pal 时进行公告。 |
| `chatBypassWait`               | bool   | 移除聊天消息之间的冷却时间。                                   |
| `chatMessageMaxLen`            | int    | 允许的最大聊天消息长度。 |
| `useWhitelist`                 | bool   | 启用 `WhiteList.json`。 |
| `whitelistMessage`             | string | 显示给非白名单玩家的消息。 |
| `steamidProtection`            | bool   | 防止使用相同 UserId 重复登录。 |
| `blockTowerBossCapture`        | bool   | 禁用高塔 Boss 捕获。 |
| `RCONbase64`                   | bool   | 启用 base64 编码的 RCON 命令。 |
| `disableIllegalItemProtection` | bool   | 禁用对改造物品的保护（例如 debug sphere）。 |
| `disableButchering`            | bool   | 禁用肢解/屠宰。 |
| `disableRenaming`              | bool   | 禁用角色重命名。 |
| `disablePalRenaming`           | bool   | 禁用 Pal 重命名。 |
| `doActionUponIllegalPalStats`  | bool   | 自动响应非法 Pal 属性 exploit。 |
| `palStatsMaxRank`              | int    | 允许的最大 Pal 强化等级（`-1` = 自动检测）。 |
| `bannedTechnologies`           | array  | 阻止学习指定科技，并在玩家加入时移除这些科技。 |
| `PalImport_Disabled`           | bool   | <span class='pd-badge pd-badge--deprecated'>已废弃</span> Pal 导入规则迁移用的旧设置。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_BanIfPalIsImpossible` | bool | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 用于不可能 Pal 导入处罚行为的旧设置。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_BannedPalIDs`       | array  | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版禁止导入 Pal ID 列表。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_AllowGenderNone`    | bool   | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 针对 `Gender: "None"` 的旧导入规则。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxLevel`           | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入最大等级。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxRank`            | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入最大伙伴技能等级。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxSoulHP`          | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入 Pal 魂生命上限。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxSoulATK`         | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入 Pal 魂攻击上限。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxSoulDEF`         | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入 Pal 魂防御上限。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxSoulCS`          | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入 Pal 魂制作速度上限。请改用 `Pals/ImportRules/Default.json`。 |
| `PalImport_MaxIV`              | int    | <span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版导入 IV 上限。请改用 `Pals/ImportRules/Default.json`。 |
