# 🛠️ `Config.json`

首次启动时，`Config.json` 会生成在 `<PalServer>/Pal/Binaries/Win64/PalDefender/`。编辑前请停止服务器，或在保存后执行 `/reloadcfg`。

!!! note "自动生成的设置"
    PalDefender 会把当前设置集写回此文件。下面未列出的键已经过时、仅用于迁移，或在当前公开构建中不可用。

## 常规与处理措施

| 键 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `version` | string | 当前版本 | 由 PalDefender 维护的配置架构/版本标记。 |
| `MOTD` | array | 三条消息 | 玩家加入时发送的消息。支持 `{ServerName}`、`{PlayerName}`、`{Difficulty}`、`{DeathPenalty}`、`{AllowGlobalPalboxExport}`、`{AllowGlobalPalboxImport}`、`{IsPvP}`、`{IsHardcore}`、`{FriendlyFire}`、`{DayTimeSpeedRate}`、`{NightTimeSpeedRate}`、`{ExpRate}`、`{PalCaptureRate}`、`{PalSpawnNumRate}`、`{PalEggDefaultHatchingTime}`、`{EnemyDropItemRate}`、`{PalStomachDecreaceRate}`、`{PalStaminaDecreaceRate}`、`{BaseCampMaxNumInGuild}`、`{SupplyDropSpan}` 和 `{MaxBuildingLimitNum}`。 |
| `exitServerOnStartupFailure` | bool | `true` | PalDefender 无法初始化时停止服务器。部分托管商可能会将其视为崩溃并反复重启。 |
| `preventAdminPasswordInChat` | bool | `true` | 阻止管理员密码作为聊天文本发送。 |
| `shouldWarnCheaters` | bool | `true` | 自动检测触发时警告玩家。 |
| `shouldWarnCheatersReason` | bool | `false` | 在警告中包含检测原因。 |
| `shouldKickCheaters` | bool | `true` | 踢出检测到的作弊者，除非启用了更强的处理措施。 |
| `shouldBanCheaters` | bool | `false` | 封禁检测到的作弊者账号。 |
| `shouldIPBanCheaters` | bool | `false` | 封禁检测到的作弊者 IP。 |
| `blockEmergencyRespawn` | bool | `true` | 阻止“菜单 → 紧急重生”。 |

## RCON 与日志

| 键 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` | 不活跃 RCON 连接超时前的秒数。 |
| `RCONbase64` | bool | `false` | 启用 Base64 编码的 RCON 命令。 |
| `logNetworking` | bool | `false` | 写入受支持的网络日志。当前公开构建已禁用网络日志功能。 |
| `logNetworkingToConsole` | bool | `true` | 网络日志可用时将其同步输出到控制台。 |
| `logChat` | bool | `true` | 记录全局、公会和 Say 聊天。 |
| `logRCON` | bool | `false` | 记录 RCON 命令。 |
| `logPlayerUID` | bool | `false` | 在相关日志和反作弊 webhook 中包含 PlayerUID。 |
| `logPlayerIP` | bool | `true` | 在相关日志和反作弊 webhook 中包含 IP 地址。 |
| `logPlayerDeaths` | bool | `true` | 记录玩家死亡和击杀。 |
| `logPlayerLogins` | bool | `true` | 记录玩家加入和离开。 |
| `logPlayerBuildings` | bool | `true` | 记录受支持的建造、取消、拆除和 Palbox 移动活动。 |
| `logPlayerSummons` | bool | `true` | 记录玩家召唤 Raid Boss。 |
| `logPlayerCaptures` | bool | `true` | 保留的兼容设置。由于可用事件不可靠，1.9.0 已禁用捕获日志。 |
| `BannedCampWorker` | array | Panthalus 变体 | 禁止分配到基地的 Character ID。匹配不区分大小写；`BOSS_...` 等变体必须单独列出。 |
| `logHelicopterKills` | bool | `true` | 记录战斗直升机击杀。 |
| `logCraftings` | bool | `true` | 记录玩家制作。 |
| `logTechUnlocks` | bool | `true` | 记录科技解锁。 |
| `logOpenOilrigBoxes` | bool | `true` | 记录 Oil Rig End Goal Box 事件。 |
| `OilrigGoalBoxLocktime` | int | `300` | Oil Rig End Goal Box 保持锁定的秒数。 |

## Discord Webhook

`PalWebhooks` 是一个对象。将某个 URL 留空即可禁用对应目标。Webhook 发送进入队列，使突发消息错开发送而不会阻塞游戏线程。

| 子键 | 发送内容 |
| --- | --- |
| `webhookURL_Chat` | 全局和 Say 聊天消息。 |
| `webhookURL_GuildChat` | 包含公会名称的公会聊天消息。 |
| `webhookURL_Commands` | 通过游戏内聊天执行的命令，包括管理员和完整命令。 |
| `webhookURL_Deaths` | 死亡和击杀。需要启用 `announcePlayerDeaths` 或 `logPlayerDeaths`。 |
| `webhookURL_JoinLeave` | 启用 `announceConnections` 时发送加入/离开事件；遵循 `dontAnnounceAdminConnections`。 |
| `webhookURL_Summons` | 玩家/管理员召唤公告以及完整的受跟踪召唤伤害结果。 |
| `webhookURL_Oilrig` | 启用对应 `announce...` 设置时发送 Oil Rig 箱子和直升机击杀。 |
| `webhookURL_AntiCheats` | 自动检测和需人工审查的反作弊检测。是否包含 UID/IP 由 `logPlayerUID` 和 `logPlayerIP` 控制。 |

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

## 管理、聊天与公告

| 键 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` | 将管理员登录/命令限制在 `adminIPs`。 |
| `adminAutoLogin` | bool | `false` | 白名单 IP 加入时自动启用管理员模式。 |
| `adminIPs` | array | `127.0.0.1` | 允许管理服务器的精确 IP 和受支持的通配符条目。 |
| `bannedChatWords` | array | 常见 RMT 词语 | 不区分大小写的聊天过滤词。 |
| `bannedNames` | array | 已知滥用名称 | 登录时拒绝的玩家名称。 |
| `allowAdminCheats` | bool | `false` | 允许管理员使用 `adminCheats` 中的命令并绕过部分防护。Admin Gun 本身只要求已启用游戏内管理员状态。 |
| `allowGodmodeOnehit` | bool | `false` | 允许 Godmode 用户造成一击必杀伤害。 |
| `adminCheats` | array | 自动生成的列表 | `allowAdminCheats` 禁用时被视为管理员作弊的命令。RCON 不受此列表限制。 |
| `announceConnections` | bool | `false` | 在聊天中公告加入/离开，并启用加入/离开 webhook 来源。 |
| `dontAnnounceAdminConnections` | bool | `true` | 在这些公告中隐藏管理员加入/离开。 |
| `announcePunishments` | bool | `false` | 公告自动作弊踢出/封禁。 |
| `announcePlayerDeaths` | bool | `false` | 在聊天中公告玩家死亡。 |
| `announceOpenOilrigBoxes` | bool | `false` | 公告 Oil Rig 箱子事件并启用其 webhook 来源。 |
| `announceHelicopterKills` | bool | `false` | 公告直升机击杀并启用其 webhook 来源。 |
| `announcePlayerSummons` | bool | `false` | 公告玩家召唤 Raid Boss。 |
| `announceAdminSummons` | bool | `false` | 公告通过管理召唤功能生成的 Pal。 |
| `announceAdminSummonsKill` | bool | `true` | 公告管理员召唤 Pal 的击杀/死亡。 |
| `chatBypassWait` | bool | `true` | 移除聊天消息之间的正常等待时间。 |
| `chatMessageMaxLen` | int | `128` | 接受的聊天消息最大长度。 |
| `useWhitelist` | bool | `false` | 启用 `WhiteList.json`。 |
| `whitelistMessage` | string | 自动生成文本 | 向被拒绝的非白名单玩家显示的消息。 |
| `steamidProtection` | bool | `true` | 拒绝同时重复使用同一个 UserId。 |

## 游戏行为验证

| 键 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | int | `100` | 允许对建筑造成的最大 PvP 伤害。 |
| `pvpMaxToPalDamage` | int | `1000` | 允许对 Pal 造成的最大 PvP 伤害。 |
| `pveMaxToPalBanThreshold` | int | `900000` | 用于作弊检测的 PvE Pal 伤害阈值。 |
| `droppedPalPickupRange` | int | `99999` | 拾取掉落 Pal 时接受的最大距离。 |
| `treeLimiter` | float | `0.1` | 树木摧毁事件之间的最小秒数，用于限制大规模植被事件。 |
| `disableIllegalItemProtection` | bool | `false` | 禁用无效/修改物品防护。 |
| `disableButchering` | bool | `false` | 阻止肢解 Pal。 |
| `disableRenaming` | bool | `false` | 阻止玩家改名。 |
| `disablePalRenaming` | bool | `false` | 阻止 Pal 改名。 |
| `doActionUponIllegalPalStats` | bool | `true` | 检测到不可能的 Pal 属性时执行配置的作弊处理。 |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` | 阻止所请求工作台不支持的配方。 |
| `preventDoctorSurgiExploit` | bool | `true` | 检测/阻止 Doctor Surgi 漏洞。 |
| `doActionUponDoctorSurgiExploit` | bool | `true` | 对该漏洞执行配置的作弊处理。 |
| `palStatsMaxRank` | int | `-1` | 最大 Pal 强化等级；`-1` 使用自动/当前游戏限制。 |
| `bannedTechnologies` | array | 空 | 阻止学习并在检测到时移除的科技 ID。 |

## 反作弊功能开关

| 键 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` | 旧 AntiDupe 功能的兼容开关；在当前公开 1.9.0 构建中无效。 |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` | 旧建造最小间隔；目前无效。 |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` | 旧拆除最小间隔；目前无效。 |
| `antiDupeShowBlockMessage` | bool | `true` | 旧阻止消息开关；目前无效。 |
| `antiDupeBuildMessage` | string | 自动生成文本 | 旧建造阻止消息；目前无效。 |
| `antiDupeDismantleMessage` | string | 自动生成文本 | 旧拆除阻止消息；目前无效。 |
| `antiVacuumEnabled` | bool | `true` | 启用远距离拾取防护。 |
| `antiVacuumBlockAutoPickup` | bool | `true` | 对普通自动拾取应用 Anti-Vacuum 检查。 |
| `antiVacuumBlockRelicObtain` | bool | `true` | 对遗物收集应用检查。 |
| `antiVacuumBlockNoteObtain` | bool | `true` | 对笔记收集应用检查。 |
| `antiVacuumBlockEggPickup` | bool | `true` | 对 Pal 蛋拾取应用检查。 |
| `antiVacuumMaxPickupDistance` | float | `800.0` | 受保护请求允许的最大拾取距离。 |
| `antiVacuumShowBlockMessage` | bool | `true` | 拾取被阻止时向玩家显示消息。 |
| `antiVacuumBlockMessage` | string | 自动生成文本 | 远距离拾取被阻止时显示的消息。 |
| `staminaCheatDetectionEnabled` | bool | `true` | 启用可疑耐力操作检测。 |
| `baseCampDupeDetectionEnabled` | bool | `true` | 启用基地复制检测。 |
| `damageCheatDetectionEnabled` | bool | `true` | 启用伤害作弊检测。 |
| `ammoCheatDetectionEnabled` | bool | `true` | 启用弹药/武器状态作弊检测。 |

为保持配置兼容，仍会生成 `antiDupe...` 键，但旧 AntiDupe 功能在当前公开 1.9.0 构建中已禁用。在该功能重新启用前，请勿依赖这些选项。

## 旧版迁移键

`PalImport_Disabled`、`PalImport_BanIfPalIsImpossible`、`PalImport_BannedPalIDs`、`PalImport_AllowGenderNone`、`PalImport_MaxLevel`、`PalImport_MaxRank`、`PalImport_MaxSoulHP`、`PalImport_MaxSoulATK`、`PalImport_MaxSoulDEF`、`PalImport_MaxSoulCS` 和 `PalImport_MaxIV` 仅用于将旧安装迁移到 [`Pals/ImportRules/Default.json`](./PalImportRules.md)。当前 `Config.json` 不再写入这些键。

旧键 `RCONUsePacketIdFix`、`bannedIPs`、`bannedMessage`、`isChineseCmd` 和 `blockTowerBossCapture` 不属于当前配置。封禁记录存储在 `Banlist.json` 中。
