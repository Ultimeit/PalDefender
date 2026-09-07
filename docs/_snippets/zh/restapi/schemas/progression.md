### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Meta` | object | 目标玩家元数据。 |
| `Progression` | object | 进度、货币、击败、捕获和活动数据。 |

`Meta` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `PlayerUID` | string | Palworld 存档数据使用的玩家 UID。 |
| `Player` | string | 请求路径中提供的玩家标识符。 |

`Progression` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Player` | object | 玩家等级、经验值和未使用的属性点。 |
| `Currencies` | object | 遗物点和科技点总计。 |
| `Bosses` | object | Boss 击败计数和标记。 |
| `Captures` | object | 帕鲁捕获和屠宰计数。 |
| `Activities` | object | 制作、地下城、钓鱼、宝藏及其他活动计数。 |

`Progression.Player` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `level` | integer | 当前玩家等级。 |
| `exp` | integer | 当前经验值。 |
| `unusedStatusPoints` | integer | 玩家未使用的属性点。 |

`Progression.Currencies` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `relics` | object | 以遗物类型为键的遗物点数总计。 |
| `technologyPoints` | integer | 科技点总计。 |
| `ancientTechnologyPoints` | integer | 古代科技点总计。 |

`Progression.Bosses` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `towerBossDefeatCounts` | object | 以 Boss ID 为键的高塔 Boss 击败次数。 |
| `normalBossDefeatFlags` | object | 以 Boss ID 为键的普通 Boss 击败标记。 |
| `raidBossDefeatCounts` | object | 以 Boss ID 为键的突袭 Boss 击败次数。 |
| `totalBossDefeatCount` | integer | 高塔 Boss 击败次数之和。 |
| `predatorDefeatCount` | integer | 掠食者击败次数。 |

`Progression.Captures` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `tribeCaptureCount` | integer | 部落捕获总数。 |
| `palCaptureCounts` | object | 以帕鲁 ID 为键的捕获次数。 |
| `palCaptureBonusCounts` | object | 以帕鲁 ID 为键的捕获奖励次数。 |
| `palButcherCounts` | object | 以帕鲁 ID 为键的屠宰次数。 |

`Progression.Activities` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `craftItemCounts` | object | 以物品 ID 为键的制作数量。 |
| `normalDungeonClearCount` | integer | 普通地下城通关次数。 |
| `fixedDungeonClearCount` | integer | 固定地下城通关次数。 |
| `oilrigClearCount` | integer | Oil Rig 通关次数。 |
| `palRankUpCounts` | object | 以帕鲁 ID 为键的升阶次数。 |
| `arenaSoloClearCounts` | object | 以竞技场 ID 为键的单人通关次数。 |
| `npcTalkCounts` | object | 以 NPC ID 为键的对话次数。 |
| `fishingCounts` | object | 以鱼类 ID 为键的钓鱼次数。 |
| `foundTreasureCount` | integer | 找到宝藏的次数。 |
| `campConqueredCount` | integer | 征服营地的次数。 |
| `firstFishingComplete` | boolean | 是否已记录首次完成钓鱼。 |
