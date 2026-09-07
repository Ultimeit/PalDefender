# 📄 `PalSummon.json`

PalSummon 文件定义一个固定地点的遭遇，可通过 `/summon <文件名>` 启动。将文件保存到 `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/`，被引用的 PalTemplate 则保存在 `Pals/Templates/`。

!!! tip "ID 查询"
    使用 [paldeck.cc/pals](https://paldeck.cc/pals) 查询 `PalID`，[paldeck.cc/passives](https://paldeck.cc/passives) 查询被动词条，[paldeck.cc/skills](https://paldeck.cc/skills) 查询模板使用的技能 ID。

## 遭遇配置键

| 键 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `PalTemplate` | string | 必填 | `Pals/Templates/` 中的模板文件名；可以省略 `.json`。 |
| `BossBattleName` | string | Pal ID | 用于公告、日志、webhook 和伤害结果的显示名称。 |
| `Uncapturable` | bool | `false` | 使召唤出的 Pal 永远无法被捕获。 |
| `CapturableAtHealthPercent` | number | `15` | Pal 的生命值达到该百分比或以下时才可捕获（`0`–`100`）。`Uncapturable` 为 `true` 时忽略。 |
| `DisableAI` | bool | `false` | 禁用普通 AI。闪避等部分被动行为仍可能发生。 |
| `DisableDamageMeter` | bool | `false` | 禁用伤害跟踪、结果窗口和排名奖励。此时会将 `Default` 奖励发给所有在线玩家。 |
| `SpawnScale` | number | `1.0` | 视觉/物理体型倍率；非正数会恢复为 `1.0`。 |
| `HealthMultiplier` | number | `1.0` | 最大生命值倍率；必须是大于零的有限数值。 |
| `DamageTakenMultiplier` | number | `1.0` | 承受伤害倍率；负数会恢复为 `1.0`。 |
| `DamageDealtMultiplier` | number | `1.0` | 造成伤害倍率；负数会恢复为 `1.0`。 |
| `X`, `Y`, `Z` | number | 必填 | 地图坐标。使用 `/getpos` 获取。 |
| `DisableStatuses` | array | 空 | 要禁用的状态名称。无效名称会被跳过。 |
| `Rewards` | object | 空 | 可选的排名和默认[奖励定义](#damage-meter-and-rewards)。 |

兼容别名 `CapturableAt`、`CapturableAtPercent` 和 `capturable_at` 也可使用。`HPMultiplier`、`AdditionalEnemyMaxHPRate`、`AdditionalEnemyReceiveDamageRate` 和 `AdditionalEnemyInflictDamageRate` 同样受支持，但建议使用表格中的名称。

## 伤害统计与奖励 {#damage-meter-and-rewards}

结果窗口显示伤害最高的五名玩家，前三名会有不同高亮，并且始终显示接收该窗口玩家自己的排名。奖励对象可以包含固定 `Drops` 和随机 `Pools`。

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

数字键代表伤害排名。`Default` 适用于没有专属排名奖励的位置。`DisableDamageMeter` 为 `true` 时，只使用 `Default`，并将其发给每位在线玩家。

对于简单的进度奖励，也可以把 `EXP`、`TechnologyPoints` 或 `AncientTechnologyPoints` 直接放在排名/默认对象中；需要与物品和 Pal 蛋组合时，使用 `Drops` 更方便。

### 奖励条目

每个条目必须且只能定义一种奖励类型：

| 奖励 | 必填字段 | 可选字段 |
| --- | --- | --- |
| 物品 | `ItemID` | `Count`（默认 `1`） |
| Pal 蛋 | `EggID`, `PalTemplate` | `Count`（默认 `1`）、`Level`（为 `0` 时使用模板等级） |
| 经验 | `EXP` | — |
| 科技点 | `TechnologyPoints` | — |
| 古代科技点 | `AncientTechnologyPoints` | — |

数量可以是固定整数，也可以写成 `{ "Min": 1, "Max": 3 }`。直接 `Drops` 可指定 `0` 到 `100` 的 `Chance`。奖励池条目在加权模式中使用 `Weight`，在 `Independent` 模式中使用 `Chance`，并且可以覆盖 `Unique`。

### 奖励池

| 奖励池键 | 默认值 | 说明 |
| --- | --- | --- |
| `Name` | 空 | 用于诊断的可选名称。 |
| `Mode` | `OneOf` | `OneOf`、`Pick`、`All` 或 `Independent`。 |
| `Chance` | `100` | 整个奖励池激活的概率。 |
| `Rolls` | `1` | `Pick` 模式的选择次数。 |
| `Unique` | `true` | 防止 `Pick` 选中重复条目；单个条目可以覆盖该设置。 |
| `Entries` | 必填 | 奖励条目数组。 |

- `OneOf` 根据 `Weight` 选择一个条目。
- `Pick` 进行 `Rolls` 次加权选择。
- `All` 发放所有条目。
- `Independent` 分别对每个条目的 `Chance` 进行判定。

```json
"Pools": [
    {
        "Name": "Rare drop",
        "Mode": "OneOf",
        "Chance": 25,
        "Entries": [
            { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 4 },
            { "EggID": "PalEgg_Dragon_05", "PalTemplate": "RaidReward.json", "Level": 50, "Weight": 1 }
        ]
    }
]
```

## 完整示例

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Arena Anubis",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "HealthMultiplier": 8.0,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "Winner bonus",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## 验证清单

1. 先使用 `/givemepal_j <模板>` 测试被引用的模板。
2. 使用 `/getpos` 获取 `X`、`Y` 和 `Z`；通过 RCON 使用 `/getpos` 时必须提供 UserId。
3. 使用有效 JSON，不要包含注释或末尾多余逗号。
4. 每个奖励条目只能使用一种奖励类型。
6. 执行 `/summon <文件名>`，并查看 PalDefender 日志中的具体验证错误。
