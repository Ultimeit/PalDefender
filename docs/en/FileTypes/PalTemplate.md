# 📄 `PalTemplate.json`

use <https://paldeck.cc/creator> to create those files way easier!

| Key                      | Type   | Description                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | string | Internal ID of the Pal to spawn. Use [this](https://paldeck.cc/pals) to retrieve the IDs.                             |
| `UniqueNPCID`            | string | Internal ID of the Pal to spawn NPCs.                                               |
| `Nickname`               | string | Optional nickname given to the Pal.                                                 |
| `SkinId`                 | string | Skin override for the Pal (used for custom appearances). Use cmd `/getskinids` to retrieve IDs. |
| `Gender`                 | string | `"Male"`, `"Female"` or `"None"`.                                                   |
| `Level`                  | int    | The level of the pal.                                                               |
| `Exp`                    | int    | Experience points.                                                                  |
| `Shiny`                  | bool   | Whether the Pal is shiny.                                                           |
| `PartnerSkillLevel`      | int    | Level of the Pal’s partner skill. Cannot be lower than 1!                           |
| `CondensedPals`          | int    | Number of Pals merged/condensed into this one.                                      |
| `UnusedStatusPoints`     | int    | Available status points for manual distribution. Probably only used for players?    |
| `HP` / `SP` / `MP`       | int    | Base Health, Stamina, and Mana values.                                              |
| `Hunger` / `MaxHunger`   | int    | Current and max hunger values.                                                      |
| `SAN`                    | int    | Sanity (mental stability of the Pal).                                               |
| `Support`                | int    | Support level (used for AI behavior and skills).                                    |
| `CraftSpeed`             | int    | Crafting speed multiplier.                                                          |
| `PalSouls`               | object | Passive soul bonuses. Contains: `Health`, `Attack`, `Defense`, `CraftSpeed`. (0-255) |
| `IVs`                    | object | Individual stat values. Contains: `Health`, `AttackMelee`, `AttackShot`, `Defense`. (0-255) |
| `ActiveSkills`           | array  | List of currently equipped skills (Max 3). Use [this](https://paldeck.cc/skill) to retrieve the IDs. |
| `LearntSkills`           | array  | Skills the Pal has learned and can swap to. (Avoid putting active skills here). Use [this](https://paldeck.cc/skill) to retrieve the IDs. |
| `Passives`               | array  | Passive traits the Pal has. Use [this](https://paldeck.cc/passives) to retrieve the IDs. |
| `ExtraWorkSuitabilities` | object | Boosted work types and levels (e.g., `"Mining": 2`). Available work types: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`.  |
| `DisableWorkPreferences` | array  | Work types the Pal refuses to do. Available work types: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Example:

This file has to be stored at: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate` can be any unique name in that folder. This will be the command argument for `/givepal_j` and `/spawnpal_j`!)

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