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