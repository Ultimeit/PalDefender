# 📄 `PalTemplate.json`

使用 <https://paldeck.cc/creator> 可以更轻松地创建这些文件！

| 键                      | 类型   | 描述                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | string | 要生成的帕鲁的内部 ID。使用[此链接](https://paldeck.cc/pals)检索 ID。                             |
| `UniqueNPCID`            | string | 用于生成 NPC 的帕鲁内部 ID。                                               |
| `Nickname`               | string | 给予帕鲁的可选昵称。                                                 |
| `SkinId`                 | string | 帕鲁的皮肤覆盖（用于自定义外观）。使用命令 `/getskinids` 检索 ID。 |
| `Gender`                 | string | `"Male"`、`"Female"` 或 `"None"`。                                                   |
| `Level`                  | int    | 帕鲁的等级。                                                               |
| `Exp`                    | int    | 经验值。                                                                  |
| `Shiny`                  | bool   | 该帕鲁是否为闪光。                                                           |
| `PartnerSkillLevel`      | int    | 帕鲁的伙伴技能等级。不能低于 1！                           |
| `CondensedPals`          | int    | 合并/凝聚到此帕鲁中的帕鲁数量。                                      |
| `UnusedStatusPoints`     | int    | 可用于手动分配的状态点。可能仅用于玩家？    |
| `HP` / `SP` / `MP`       | int    | 基础生命值、耐力值和魔法值。                                              |
| `Hunger` / `MaxHunger`   | int    | 当前和最大饥饿值。                                                      |
| `SAN`                    | int    | 理智值（帕鲁的精神稳定性）。                                               |
| `Support`                | int    | 支援等级（用于 AI 行为和技能）。                                    |
| `CraftSpeed`             | int    | 制作速度倍数。                                                          |
| `PalSouls`               | object | 被动灵魂加成。包含：`Health`、`Attack`、`Defense`、`CraftSpeed`。（0-255） |
| `IVs`                    | object | 个体数值。包含：`Health`、`AttackMelee`、`AttackShot`、`Defense`。（0-255） |
| `ActiveSkills`           | array  | 当前装备的技能列表（最多 3 个）。使用[此链接](https://paldeck.cc/skill)检索 ID。 |
| `LearntSkills`           | array  | 帕鲁已学习并可切换的技能。（避免将主动技能放在这里）。使用[此链接](https://paldeck.cc/skill)检索 ID。 |
| `Passives`               | array  | 帕鲁拥有的被动特性。使用[此链接](https://paldeck.cc/passives)检索 ID。 |
| `ExtraWorkSuitabilities` | object | 提升的工作类型和等级（例如，`"Mining": 2`）。可用工作类型：`EmitFlame`、`Watering`、`Seeding`、`GenerateElectricity`、`Handcraft`、`Collection`、`Deforest`、`Mining`、`OilExtraction`、`ProductMedicine`、`Cool`、`Transport`、`MonsterFarm`。  |
| `DisableWorkPreferences` | array  | 帕鲁拒绝执行的工作类型。可用工作类型：`BaseCampBattle`、`EmitFlame`、`Watering`、`Seeding`、`GenerateElectricity`、`Handcraft`、`Collection`、`Deforest`、`Mining`、`OilExtraction`、`ProductMedicine`、`Cool`、`Transport`、`MonsterFarm`。 |

## 示例：

此文件必须存储在：`<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
（`ExamplePalTemplate` 可以是该文件夹中的任何唯一名称。这将是 `/givepal_j` 和 `/spawnpal_j` 的命令参数！）

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
