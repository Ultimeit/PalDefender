# :octicons-file-16: `PalTemplate.json`

可以使用 <https://paldeck.cc/creator> 更轻松地创建这些文件。

!!! tip "ID 查询"
    使用 [paldeck.cc/pals](https://paldeck.cc/pals) 查询 `PalID`，使用 [paldeck.cc/passives](https://paldeck.cc/passives) 查询 `Passives`，使用 [paldeck.cc/skills](https://paldeck.cc/skills) 查询 `ActiveSkills` 和 `LearntSkills`。

| 键                      | 类型   | 描述                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | string | 要生成的 Pal 内部 ID。可在 Paldeck 查询有效的 [`PalID`](https://paldeck.cc/pals)。 |
| `UniqueNPCID`            | string | 要生成 NPC Pal 时使用的内部 ID。 |
| `Nickname`               | string | 给 Pal 设置的可选昵称。 |
| `SkinId`                 | string | 帕鲁皮肤覆盖（用于自定义外观）。使用 `/getskinids` 获取 ID。 |
| `Gender`                 | string | `"Male"`、`"Female"` 或 `"None"`。 |
| `Level`                  | int    | 帕鲁等级。                                                               |
| `Exp`                    | int    | 经验值。 |
| `Shiny`                  | bool   | 该 Pal 是否为闪光。 |
| `PartnerSkillLevel`      | int    | Pal 伙伴技能等级。不能低于 1！ |
| `CondensedPals`          | int    | 已浓缩/合并到这只 Pal 中的 Pals 数量。 |
| `UnusedStatusPoints`     | int    | 可手动分配的未使用属性点，可能主要用于玩家。 |
| `FriendshipPoints`       | int    | Pal 的友好度数值。 |
| `PhysicalHealth`         | string | 身体健康状态。有效名称包括 `Healthful`、`MinorInjury`、`Severe`、`Dying`、`DeadBody`、`CloudCemetery`。 |
| `WorkerSick`             | string | 工作疾病状态。有效名称包括 `None`、`Cold`、`Sprain`、`Bulimia`、`GastricUlcer`、`Fracture`、`Weakness`、`DepressionSprain`、`DisturbingElement`。 |
| `ImportedCharacter`      | bool   | 将该 Pal 标记为导入角色。 |
| `HP` / `SP` / `MP`       | number | 基础生命、耐力和法力值。 |
| `Shield`                 | number | 护盾值。 |
| `Hunger` / `MaxHunger`   | int    | 当前饥饿值和最大饥饿值。 |
| `SAN`                    | int    | SAN 值，即 Pal 的精神稳定度。 |
| `Support`                | int    | 支援等级，用于 AI 行为和技能。 |
| `CraftSpeed`             | int    | 制作速度倍率。 |
| `PalSouls`               | object | Pal 魂强化加成。包含 `Health`、`Attack`、`Defense`、`CraftSpeed`。建议的正常值由你的导入规则控制。 |
| `IVs`                    | object | 个体值。包含 `Health`、`AttackMelee`、`AttackShot`、`Defense`。建议的正常值由你的导入规则控制。 |
| `ActiveSkills`           | array  | 当前装备的技能列表（最多 3 个）。如果提供超过 3 个，额外条目会被视为已学会技能。可在 Paldeck 查询有效的 [skill IDs](https://paldeck.cc/skills)。 |
| `LearntSkills`           | array  | Pal 已学会并可切换的技能。避免把当前装备技能放在这里。可在 Paldeck 查询有效的 [skill IDs](https://paldeck.cc/skills)。 |
| `Passives`               | array  | Pal 拥有的被动词条。普通 Pal 最多应使用 4 个被动。可在 Paldeck 查询有效的 [`PassiveID`](https://paldeck.cc/passives)。 |
| `ExtraWorkSuitabilities` | object | 增强的工作类型和等级（例如 `"Mining": 2`）。可用工作类型：`EmitFlame`、`Watering`、`Seeding`、`GenerateElectricity`、`Handcraft`、`Collection`、`Deforest`、`Mining`、`OilExtraction`、`ProductMedicine`、`Cool`、`Transport`、`MonsterFarm`。 |
| `DisableWorkPreferences` | array  | Pal 拒绝从事的工作类型。可用工作类型：`BaseCampBattle`、`EmitFlame`、`Watering`、`Seeding`、`GenerateElectricity`、`Handcraft`、`Collection`、`Deforest`、`Mining`、`OilExtraction`、`ProductMedicine`、`Cool`、`Transport`、`MonsterFarm`。 |

## 操作说明

1. 在 `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/` 中为每个自定义 Pal 创建一个 JSON 文件。
2. 使用唯一文件名，例如 `RaidRewardAnubis.json`。命令通常可使用 `RaidRewardAnubis` 或 `RaidRewardAnubis.json`。
3. 必须始终包含 `PalID`。其他字段都是可选的；缺失值会使用 PalDefender 或 Palworld 的默认值。
4. `Level` 和 `PartnerSkillLevel` 都必须为 `1` 或更高。
5. `ActiveSkills` 中只放 3 个已装备攻击技能；额外已学会技能放入 `LearntSkills`。
6. 帕鲁、技能、被动、皮肤和工作类型必须使用精确 ID。错误 ID 可能导致导入失败或被忽略。
7. 上传前验证 JSON。JSON 不允许注释或末尾多余逗号。
8. 如果模板可以导入，但某些值被修改或阻止，请检查服务器的 `Pals/ImportRules/Default.json` 以及任何单个 Pal 覆盖文件。

## 设置步骤

1. 先确定模板用途：简单管理员奖励、活动 Boss、测试 Pal，或用于召唤文件的生成模板。
2. 在 [paldeck.cc/pals](https://paldeck.cc/pals) 选择 `PalID`。显示名称不一定是文件 ID，请准确复制 ID。
3. 只添加你想控制的字段。短模板比大型模板更容易排查问题。
4. 在 [paldeck.cc/skills](https://paldeck.cc/skills) 选择技能。三个已装备攻击技能放入 `ActiveSkills`；额外已学会技能放入 `LearntSkills`。
5. 在 [paldeck.cc/passives](https://paldeck.cc/passives) 选择被动。正常用法下最多保留四个被动，除非你的服务器有意允许更多。
6. 将文件保存到 `Pal/Binaries/Win64/PalDefender/Pals/Templates/`。
7. 先用 `/givemepal_j <filename>` 测试。之后同一个模板可用于 `/givepal_j`、`/spawnpal_j`、`/giveegg_j`、REST API 或 `PalSummon.json`。

## 示例说明

下面的最小示例会创建一只 50 级 Anubis，装备三个攻击技能和两个被动。它只包含必需的 `PalID` 和少量常用字段，适合测试。

较大的示例刻意设置得比较极端，用于展示 souls、IV、技能、被动和工作适应性覆盖值的可用结构。在启用导入规则的服务器上，高数值可能会被限制或阻止。

## 最小示例

```json
{
    "PalID": "Anubis",
    "Nickname": "Arena Anubis",
    "Gender": "None",
    "Level": 50,
    "PartnerSkillLevel": 1,
    "HP": 3500,
    "SAN": 100,
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "RockLance"
    ],
    "Passives": [
        "Legend",
        "CraftSpeed_up3"
    ]
}
```

## 示例

该文件必须保存到：`<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
（`ExamplePalTemplate` 可以是该文件夹中任意唯一名称。它将作为 `/givepal_j` 和 `/spawnpal_j` 的命令参数！）

```json
{
    "PalID": "Anubis",
    "Nickname": "OPnubis",
    "Gender": "None",
    "Level": 255,
    "Shiny": true,
    "PartnerSkillLevel": 255,
    "HP": 999999,
    "SP": 999999,
    "MP": 999999,
    "Hunger": 999999,
    "MaxHunger": 999999,
    "SAN": 999999,
    "Support": 999999,
    "CraftSpeed": 999999,
    "PalSouls": {
        "Health": 255,
        "Attack": 255,
        "Defense": 255,
        "CraftSpeed": 255
    },
    "IVs": {
        "Health": 255,
        "AttackMelee": 255,
        "AttackShot": 255,
        "Defense": 255
    },
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "Unique_Anubis_LowRoundKick"
    ],
    "Passives": [
        "Legend",
        "PAL_ALLAttack_up3",
        "Deffence_up3",
        "Vampire",
        "Stamina_Up_3",
        "EternalFlame",
        "PAL_Sanity_Down_3",
        "Invader",
        "SwimSpeed_up_3",
        "Rare",
        "Nushi",
        "PAL_FullStomach_Down_3",
        "CraftSpeed_up3",
        "Salvation",
        "Witch",
        "MoveSpeed_up_3",
        "SwimSpeed_up_2",
        "CraftSpeed_up2",
        "Deffence_up2",
        "ElementBoost_Normal_2_PAL",
        "PAL_FullStomach_Down_2",
        "ElementBoost_Dragon_2_PAL",
        "ElementBoost_Earth_2_PAL",
        "PAL_ALLAttack_up2",
        "ElementBoost_Fire_2_PAL",
        "ElementBoost_Ice_2_PAL",
        "Stamina_Up_1",
        "TrainerLogging_up1",
        "ElementBoost_Thunder_2_PAL",
        "ElementBoost_Aqua_2_PAL",
        "ElementBoost_Dark_2_PAL",
        "TrainerMining_up1",
        "TrainerWorkSpeed_UP_1",
        "SalePrice_Up_1",
        "Test_PalEgg_HatchingSpeed_Up",
        "MoveSpeed_up_2",
        "CoolTimeReduction_Up_1",
        "ElementBoost_Leaf_2_PAL",
        "TrainerDEF_UP_1",
        "TrainerATK_UP_1",
        "PAL_Sanity_Down_2",
        "ElementResist_Normal_1_PAL",
        "ElementBoost_Dragon_1_PAL",
        "ElementResist_Leaf_1_PAL",
        "PAL_ALLAttack_up1",
        "ElementBoost_Thunder_1_PAL",
        "ElementResist_Dark_1_PAL",
        "ElementBoost_Ice_1_PAL",
        "PAL_FullStomach_Down_1",
        "ElementResist_Dragon_1_PAL",
        "ElementResist_Earth_1_PAL",
        "SalePrice_Up_2",
        "Stamina_Up_2",
        "ElementBoost_Leaf_1_PAL",
        "Deffence_up1",
        "ElementResist_Ice_1_PAL",
        "ElementBoost_Aqua_1_PAL",
        "CoolTimeReduction_Up_2",
        "ElementResist_Thunder_1_PAL",
        "MoveSpeed_up_1",
        "Alien",
        "PAL_Sanity_Down_1",
        "ElementBoost_Earth_1_PAL",
        "ElementBoost_Fire_1_PAL",
        "CraftSpeed_up1",
        "SwimSpeed_up_1",
        "ElementResist_Fire_1_PAL",
        "ElementBoost_Dark_1_PAL",
        "ElementResist_Aqua_1_PAL",
        "ElementBoost_Normal_1_PAL"
    ],
    "ExtraWorkSuitabilities": {
        "EmitFlame": 5,
        "Watering": 5,
        "Seeding": 5,
        "GenerateElectricity": 5,
        "Handcraft": 5,
        "Collection": 5,
        "Deforest": 5,
        "Mining": 5,
        "OilExtraction": 5,
        "ProductMedicine": 5,
        "Cool": 5,
        "Transport": 5,
        "MonsterFarm": 5,
        "Anyone": 5
    }
}
```
