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
| `DamageTakenMultiplier` | number | `1.0` | 承受伤害倍率；负数会恢复为 `1.0`。 |
| `DamageDealtMultiplier` | number | `1.0` | 造成伤害倍率；负数会恢复为 `1.0`。 |
| `X`, `Y`, `Z` | number | 必填 | 地图坐标。使用 `/getpos` 获取。 |
| `DisableStatuses` | array | 空 | 要禁用的状态名称。无效名称会被跳过。 |
| `Rewards` | object 或 array | 空 | 可选的排名奖励和[默认奖励定义](#damage-meter-and-rewards)。推荐使用 object 形式。 |

兼容别名 `CapturableAt`、`CapturableAtPercent` 和 `capturable_at` 也可使用。`AdditionalEnemyReceiveDamageRate` 和 `AdditionalEnemyInflictDamageRate` 同样受支持，但建议使用表格中的名称。

!!! warning "最大生命值迁移"
    召唤出的帕鲁的最大生命值现在取自所引用 PalTemplate 中的 `HP`。`HealthMultiplier`、`HPMultiplier` 和 `AdditionalEnemyMaxHPRate` 已不再受支持；请从现有 PalSummon 文件中删除这些字段。

## 伤害统计与奖励 { #damage-meter-and-rewards }

召唤的帕鲁死亡或被捕获后会结算奖励。伤害排行榜按伤害从高到低排序。结果窗口显示前五名并突出显示前三名；如果接收结果的玩家不在前五名中，还会显示其自己的名次。

启用伤害跟踪后，每个参与玩家的处理方式如下：

1. PalDefender 查找与该玩家的最终排名匹配的数字 `Rewards` 键。
2. 如果该确切排名不存在，则 PalDefender 使用 `Rewards.Default`。
3. 如果两者都不存在，则该玩家不会获得任何奖励。
4. 为该玩家单独随机结算所选奖励。因此，使用相同 `Default` 定义的两名玩家可能获得不同的随机结果。

只有在战斗结束时仍然在线并且拥有可用玩家控制器的参与者才能获得排名奖励。编号奖励不包括 `Default` 奖励；它会取代该等级。

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

在此示例中，第一名会收到保证掉落的物品，第二名会收到随机数量的 EXP，而其他排名的参与者独立地有 75% 的机会收到 1,000 Money。

排名键必须是写为 JSON 对象键的正整数，例如 `"1"`、`"2"` 或 `"10"`。 `"0"`、负排名和任意名称均无效。 `Default` 不区分大小写进行匹配。

??? note "数组形式"
    `Rewards` 也可以是一个数组。数组元素 0 的等级为 1，元素 1 的等级为 2，依此类推。数组形式无法定义`Default`，因此对象形式更清晰，推荐使用。

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### 奖励定义结构

每个等级和 `Default` 都包含一个奖励定义。定义可以包含两者：

- `Drops`：直接且独立评估的条目。
- `Pools`：控制如何选择条目的组。

它还可能包含级数简写 `EXP`、`TechnologyPoints` 和 `AncientTechnologyPoints`。当不需要自己的 `Chance`、`Weight` 或 `Unique` 设置时，速记是有保证的并且很有用。

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### 奖励条目类型

每个条目必须准确定义一种奖励类型。不要将项目、蛋和进度字段合并在同一条目中。

|奖励 |必填字段 |可选字段 |笔记|
| --- | --- | --- | --- |
| 物品 | `ItemID` | `Count`、`Chance`、`Weight`、`Unique` | `Count` 默认为 `1`。 |
| 帕鲁蛋 | `EggID`、`PalTemplate` | `Count`、`Level`、`Chance`、`Weight`、`Unique` | `Count` 默认为 `1`；`Level: 0` 使用模板中的等级。 |
|经验| `EXP` | `Chance`、`Weight`、`Unique` | `EXP` 值是金额或范围。 |
|技术要点| `TechnologyPoints` | `Chance`、`Weight`、`Unique` |字段值是金额或范围。 |
|古代科技点| `AncientTechnologyPoints` | `Chance`、`Weight`、`Unique` |字段值是金额或范围。 |

`Chance`、`Weight` 和 `Unique` 仅在下述上下文中有效。解析器接受的字段并不意味着它会影响每种分发模式。

建议使用上面的规范字段名称。解析器还接受这些别名：

|规范领域 |接受的别名 |
| --- | --- |
| `ItemID` | `ItemId`、`ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`、`Num` |
| `EXP` | `Exp`、`Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### 固定值、范围和机会

金额可以是固定整数或包含范围：

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- `Count`、EXP 和技术点数量必须至少为 `1` 的整数。
- 范围需要 `Min` 和 `Max`，并且 `Max` 不得低于 `Min`。
- 诸如 `"1-3"` 之类的文本范围无效；使用 `{ "Min": 1, "Max": 3 }`。
- 帕鲁蛋的 `Level` 可以为 `0`，此时沿用引用 PalTemplate 中的等级。大于 `0` 的固定等级或范围会覆盖模板等级，发放时最高限制为 255 级。
- `Chance` 接受带有可选 `%` 的数字或数字文本，例如 `30`、`30.5` 或 `"30%"`。
- `Chance: 0` 永远不会成功，`Chance: 100` 始终会成功，并且值必须保持在 `0` 和 `100` 之间。
- 对于严格介于 0 到 100 之间的机会，生成的掷骰必须低于配置的值。因此，恰好 `30.0` 的一卷失败了 `30` 的 `Chance`。

### 直接掉落

`Drops` 中的每个条目都是独立评估的。相邻条目之间不存在单选关系。缺少 `Chance` 意味着 `100`。

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

Money 是有保证的。弹药、EXP 和技术点各有自己的机会掷骰。零次、一次、两次或所有三个可选滴都可能成功。

`Weight` 和 `Unique` 不能直接在 `Drops` 中工作并产生警告。使用 `Chance` 进行可选的直接删除。

## 战利品池

奖励池首先判定自身的 `Chance`。如果判定失败，则不会处理其中任何条目；如果成功，则由 `Mode` 决定如何处理条目。

|泳池钥匙|类型 |默认|描述 |
| --- | --- | --- | --- |
| `Name` |字符串|空 |可选的诊断标签。不影响选择。 |
| `Mode` |字符串| `OneOf` | `OneOf`、`Pick`、`All` 或 `Independent`。匹配不区分大小写。 |
| `Chance` |数字或百分比文本| `100` |整个池激活的机会。 |
| `Rolls` |整数 | `1` | `Pick` 中的选择数；被其他模式忽略。 |
| `Unique` |布尔 | `true` | `Pick` 的默认重复策略；一个条目可能会覆盖它。 |
| `Entries` |数组|必填 |奖励条目非空列表。 |

`One` 被接受作为 `OneOf` 的别名，`PickN` 被接受作为 `Pick` 的别名，但建议使用规范模式名称。

|模式|可以授予多少条目？ |使用`Weight`？ |使用条目 `Chance`？ |使用 `Rolls` / `Unique`？ |
| --- | --- | --- | --- | --- |
| `OneOf` |如果池成功则恰好为 1 |是的 |没有 |没有 |
| `Pick` |最多 `Rolls` 个选择 |是的 |没有 |是的 |
| `All` |如果池成功，则每个条目一次 |没有 |没有 |没有 |
| `Independent` |所有条目归零|没有 |是的 |没有 |

All 四种模式仍然使用池级 `Chance`。一个奖励定义中的多个池是独立处理的，它们的结果将添加到直接 `Drops` 中。

### `OneOf`：一个加权结果

`OneOf` 是默认模式。如果其池级机会成功，则仅选择一个条目。条目的概率是其 `Weight` 除以所有条目权重的总和。

```json
{
    "Pools": [
        {
            "Name": "Equipment jackpot",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

权重总计为 20。在奖励池已激活的前提下，四个条目的概率分别为 35%、35%、25% 和 5%。由于奖励池本身只有 35% 的激活概率，因此帕鲁蛋的绝对概率为 `35% × 5% = 1.75%`。

- 缺少 `Weight` 默认为 `1`。
- `Weight` 必须是至少 `1` 的整数；删除条目而不是分配权重 `0`。
- `Rolls` 被忽略并产生警告，因为 `OneOf` 始终选择一次。
- 入门级 `Chance` 被忽略并产生警告。使用 `Weight` 控制相对选择概率。
- `Unique` 没有实际作用，因为只选择了一项。

### `Pick`：不重复的多个加权结果

`Pick` 重复加权选择 `Rolls` 次。使用默认的 `Unique: true` 时，选定的条目将在下一次选择之前被删除，并且无法再次选择。每次选择后，都会根据剩余条目重新计算权重。

```json
{
    "Pools": [
        {
            "Name": "Choose two different rewards",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

这将授予两个不同的条目。如果 `Rolls` 大于可用唯一条目的数量，则当没有条目剩余时，选择将停止；这不是一个错误。

### `Pick`：允许重复结果

将池的 `Unique` 设为 `false`，已选中的条目就能在后续抽取中再次被选中。相同物品的重复结果会在发放前合并。

```json
{
    "Pools": [
        {
            "Name": "Three supply rolls",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

All 三卷可能会选择Money，也可能全部选择弹药，或者结果可能会混合。例如，选择两次 Money 会产生一次 10,000 的 Money 授权，而不是两次单独的授权。

### `Pick`：覆盖每个条目的 `Unique`

条目级 `Unique` 仅覆盖该条目的池默认值。这允许在同一池中重复使用普通奖励和一次性头奖奖励。

```json
{
    "Pools": [
        {
            "Name": "Repeatable currency with unique jackpots",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

Money 在被选择后仍保留在候选列表中，因为其条目为 `Unique: false`。盔甲和头盔从池中继承 `Unique: true` ，并在选择后删除。反之亦然：池可以使用 `Unique: false`，而特定条目则使用 `Unique: true`。

### `All`：授予每个条目

当池级 `Chance` 成功时，`All` 只授予每个条目一次。

```json
{
    "Pools": [
        {
            "Name": "Complete reward bundle",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`Weight`、入门级`Chance` 和`Unique` 不影响`All`。 `Rolls` 被忽略并产生警告。要使整个捆绑包可选，请设置池的 `Chance`;要使单个条目可选，请改用 `Independent` 或直接 `Drops` 。

### `Independent`：分别判定每个条目

`Independent` 检查每个条目并使用每个条目自己的 `Chance`。它可以不授予任何条目、授予一个条目、授予多个条目或授予所有条目。

```json
{
    "Pools": [
        {
            "Name": "Independent bonus rolls",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

首先，奖励池有 80% 的概率激活。激活后，Money 条目因省略 `Chance` 而必定发放；另外三个条目分别独立判定 50%、10% 和 5% 的概率。

- 缺少条目 `Chance` 默认为 `100`。
- `Weight` 和 `Unique` 不影响此模式。
- `Rolls` 被忽略并产生警告，因为每个条目都会检查一次。

### 组合直接掉落与多个奖励池

当一个接收者应该收到多个独立结构的奖励层时，请使用多个池。

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "One equipment item",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "Two supply rolls",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "Rare independent bonuses",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

直接 Money 和 EXP 始终适用。第一个池添加一个设备项目，第二个池进行两个带替换的加权供应选择，第三个池进行两个独立的奖励掷骰。玩家可以收到每个池的结果，因为池之间不会相互竞争。

### 帕鲁蛋奖励

帕鲁蛋需要同时指定 `EggID` 和 `PalTemplate`。模板从 `Pals/Templates/` 加载，文件名中的 `.json` 可以省略。`Count` 控制发放的蛋数量。`Level: 0` 或省略等级时沿用模板等级；大于 `0` 的固定值或范围会覆盖模板等级。

```json
{
    "Pools": [
        {
            "Name": "One random egg reward",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

如果授予奖励时无法导入彩蛋模板，PalDefender 会记录错误并跳过该彩蛋奖励。

### 合并重复结果

直接掉落和所有奖励池的结果会在发放前合并：

- 具有相同 `ItemID` 的项目通过添加其计数来合并。
- 仅当 `EggID`、`PalTemplate` 和随机得到的 `Level` 全部相同时，帕鲁蛋才会合并。
- EXP、科技点、古代科技点相加。
- 可授予的项目和技术点总数被限制为带符号的 32 位最大值 (`2,147,483,647`)。

这意味着重复的 `Pick` 结果不会在奖励请求中创建重复的物品行。随机等级不同的帕鲁蛋仍会作为独立奖励发放。

### `DisableDamageMeter` 分布

当 `DisableDamageMeter` 为 `true` 时，PalDefender 不会生成伤害排行榜，也不会使用数字排名奖励。它会改为给**遭遇结束时在线的每位玩家**分别随机结算 `Rewards.Default`，其中也包括未对召唤帕鲁造成伤害的玩家。

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

每名在线玩家都会获得 Money。两种可选点数奖励会为每名玩家分别独立判定。如果 `Default` 缺失或为空，则此模式下不会发放任何奖励，PalDefender 会在日志中写入警告。

### 无效和被忽略的组合

无效的奖励数据会阻止加载 PalSummon 文件。未知或上下文忽略的字段会产生警告，因此拼写错误和无效设置会在 PalDefender 日志中可见。

|配置|结果 |
| --- | --- |
|一项同时包含 `ItemID` 和 `EXP` |错误：一个条目只能定义一种奖励类型。 |
|奖励条目没有物品、彩蛋或进度字段 |错误：PalDefender 不知道要授予什么。 |
| `Count: 0`、`Weight: 0` 或 `Rolls: 0` |错误：这些值必须至少为 `1`。 |
|范围省略 `Min` 或 `Max`，或具有 `Max < Min` |错误。 |
| `Chance` 位于 `0`–`100` 之外 |错误。 |
|池没有 `Entries`、空 `Entries` 数组或非数组值 |错误。 |
| `Chance` 放置在 `OneOf`、`Pick` 或 `All` 条目上 |警告;进入机会被忽略。 |
| `Rolls` 在 `OneOf`、`All` 或 `Independent` 上设置 |警告; `Rolls` 被忽略。 |
| `Weight` 或 `Unique` 直接放置在 `Drops` | 中警告;使用 `Chance` 进行直接删除。 |
|存在未知字段，如 `Wieght` |警告;该字段未使用。 |

使用有效的 JSON ，不带注释或尾随逗号。即使召唤仍在加载，也要查看加载警告：警告通常会识别出无效的设置。

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
5. 确认每个池都有非空的 `Entries` array，并且只使用对所选 `Mode` 生效的字段。
6. 执行 `/summon <文件名>`，并查看 PalDefender 日志中的具体验证错误和警告。
