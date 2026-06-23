# 📄 `PalTemplate.json`

use <https://paldeck.cc/creator> to create those files way easier!

!!! note "<span class='pd-badge pd-badge--beta'>Beta</span>"
    Newly documented keys and instructions on this page are marked with <span class='pd-badge pd-badge--beta'>Beta</span>. They describe user-facing file behavior and may still be refined as the wiki is improved.

!!! tip "<span class='pd-badge pd-badge--beta'>Beta</span> ID lookup"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) for `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) for `Passives`, and [paldeck.cc/skills](https://paldeck.cc/skills) for `ActiveSkills` and `LearntSkills`.

| Key                      | Type   | Description                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | string | Internal ID of the Pal to spawn. Search valid [`PalID`](https://paldeck.cc/pals) values on Paldeck. |
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
| `FriendshipPoints`       | int    | <span class='pd-badge pd-badge--beta'>Beta</span> Friendship value for the Pal.                                               |
| `PhysicalHealth`         | string | <span class='pd-badge pd-badge--beta'>Beta</span> Physical health state. Valid names include `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick`             | string | <span class='pd-badge pd-badge--beta'>Beta</span> Worker sickness state. Valid names include `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter`      | bool   | <span class='pd-badge pd-badge--beta'>Beta</span> Marks the Pal as an imported character.                                    |
| `HP` / `SP` / `MP`       | number | Base Health, Stamina, and Mana values.                                              |
| `Shield`                 | number | <span class='pd-badge pd-badge--beta'>Beta</span> Shield value.                                                              |
| `Hunger` / `MaxHunger`   | int    | Current and max hunger values.                                                      |
| `SAN`                    | int    | Sanity (mental stability of the Pal).                                               |
| `Support`                | int    | Support level (used for AI behavior and skills).                                    |
| `CraftSpeed`             | int    | Crafting speed multiplier.                                                          |
| `PalSouls`               | object | Passive soul bonuses. Contains: `Health`, `Attack`, `Defense`, `CraftSpeed`. Recommended normal values are controlled by your import rules. |
| `IVs`                    | object | Individual stat values. Contains: `Health`, `AttackMelee`, `AttackShot`, `Defense`. Recommended normal values are controlled by your import rules. |
| `ActiveSkills`           | array  | List of currently equipped skills (Max 3). If more than 3 are provided, the extra entries are treated as learned skills. Search valid [skill IDs](https://paldeck.cc/skills) on Paldeck. |
| `LearntSkills`           | array  | Skills the Pal has learned and can swap to. Avoid putting active skills here. Search valid [skill IDs](https://paldeck.cc/skills) on Paldeck. |
| `Passives`               | array  | Passive traits the Pal has. Normal Pals should use up to 4 passives. Search valid [`PassiveID`](https://paldeck.cc/passives) values on Paldeck. |
| `ExtraWorkSuitabilities` | object | Boosted work types and levels (e.g., `"Mining": 2`). Available work types: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`.  |
| `DisableWorkPreferences` | array  | Work types the Pal refuses to do. Available work types: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## <span class='pd-badge pd-badge--beta'>Beta</span> instruction set

1. Create one JSON file per custom Pal in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Use a unique filename, for example `RaidRewardAnubis.json`. Commands can usually use `RaidRewardAnubis` or `RaidRewardAnubis.json`.
3. Always include `PalID`. Everything else is optional, but missing values use PalDefender or Palworld defaults.
4. Keep `Level` at `1` or higher and `PartnerSkillLevel` at `1` or higher.
5. Put only the 3 equipped attacks in `ActiveSkills`; put extra known attacks in `LearntSkills`.
6. Use exact IDs for Pals, skills, passives, skins, and work types. Wrong IDs may fail to import or may be ignored.
7. Validate JSON before uploading. JSON does not allow comments or trailing commas.
8. If a template imports but values are changed or blocked, check the server's `Pals/ImportRules/Default.json` and any per-Pal override files.

## <span class='pd-badge pd-badge--beta'>Beta</span> setup walkthrough

1. Decide what the template is for: a simple admin reward, an event boss, a testing Pal, or a spawn template for a summon.
2. Pick the `PalID` at [paldeck.cc/pals](https://paldeck.cc/pals). The display name is not always the file ID, so copy the ID exactly.
3. Add only the fields you want to control. A short template is easier to debug than a very large one.
4. Choose skills from [paldeck.cc/skills](https://paldeck.cc/skills). Put the three equipped attacks in `ActiveSkills`; add extra known attacks to `LearntSkills`.
5. Choose passives from [paldeck.cc/passives](https://paldeck.cc/passives). For normal usage, keep up to four passives unless your server intentionally allows more.
6. Save the file in `Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
7. Test with `/givemepal_j <filename>` first. After that, use the same template for `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, the REST API, or `PalSummon.json`.

## <span class='pd-badge pd-badge--beta'>Beta</span> example explanations

The minimal example below creates a level 50 Anubis with three equipped attacks and two passives. It is suitable for testing because it has only the required `PalID` plus a few common fields.

The larger example is intentionally extreme. It shows the available structure for souls, IVs, skills, passives, and work suitability overrides. On servers using import rules, high values may be clamped or blocked.

## Minimal <span class='pd-badge pd-badge--beta'>Beta</span> example

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

## Example

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
