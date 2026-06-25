### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Meta` | object | Target player metadata and Pal counts. |
| `Pals` | object | Team, Palbox, and base camp Pals for the target player. |

`Meta` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `PlayerUID` | string | Player UID used by Palworld save data. |
| `Player` | string | Player identifier supplied in the request path. |
| `TeamCount` | integer | Number of Pals in the player team. |
| `PalboxCount` | integer | Number of Pals in the player Palbox. |
| `BaseCampCount` | integer | Number of base camps included. |

`Pals` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Team` | object | Team Pals keyed by Pal instance ID. |
| `Palbox` | object | Palbox Pals keyed by Pal instance ID. |
| `BaseCamps` | object[] | Guild base camps and their assigned worker Pals. |

Pal object schema:

| Field | Type | Description |
|-------|------|-------------|
| `PalID` | string | Pal species identifier. |
| `UniqueNPCID` | string | Unique NPC ID, when present. |
| `Nickname` | string | Custom Pal nickname, or an empty string. |
| `SkinId` | string | Skin ID, or an empty string. |
| `Gender` | string | Pal gender. |
| `Level` | integer | Pal level. |
| `Exp` | integer | Pal EXP. |
| `Shiny` | boolean | Whether this is a rare Pal. |
| `PartnerSkillLevel` | integer | Partner skill rank. |
| `CondensedPals` | integer | Condense rank progress. |
| `UnusedStatusPoints` | integer | Unused Pal status points. |
| `FriendshipPoints` | integer | Friendship point value. |
| `PhysicalHealth` | string | Physical health state. |
| `WorkerSick` | string | Worker sickness state. |
| `ImportedCharacter` | boolean | Whether this is marked as imported. |
| `HP` | number | Current HP. |
| `MP` | number | Current MP, when present. |
| `SP` | number | Current stamina, when present. |
| `Shield` | number | Current shield value, when present. |
| `Hunger` | number | Current hunger value. |
| `MaxHunger` | number | Maximum hunger value. |
| `SAN` | number | Sanity value. |
| `Support` | integer | Support value. |
| `CraftSpeed` | integer | Craft speed value. |
| `PalSouls` | object | Pal soul ranks with `Health`, `Attack`, `Defense`, and `CraftSpeed`. |
| `IVs` | object | IV values with `Health`, `AttackMelee`, `AttackShot`, and `Defense`. |
| `ActiveSkills` | string[] | Equipped active skills. |
| `LearntSkills` | string[] | Learned skills. |
| `Passives` | string[] | Passive skill IDs. |
| `ExtraWorkSuitabilities` | object | Additional work suitability ranks keyed by suitability ID. |
| `DisableWorkPreferences` | string[] | Disabled work preference IDs. |
| `team_slot_index` | integer | Team slot index, only on `Team` Pals. |
| `page` | integer | Palbox page index, only on `Palbox` Pals. |
| `slot` | integer | Palbox slot index, only on `Palbox` Pals. |
| `base_camp_slot_index` | integer | Base camp worker slot index, only on base camp Pals. |

`BaseCamps[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Base camp GUID. |
| `level` | integer | Base camp level. |
| `world_pos` | object | Base camp world coordinates. |
| `map_pos` | object | Converted map coordinates. |
| `state` | string | Current base camp state. |
| `pals` | object | Base camp worker Pals keyed by Pal instance ID. |

Coordinate object schema:

| Field | Type | Description |
|-------|------|-------------|
| `x` | number | X coordinate. |
| `y` | number | Y coordinate. |
| `z` | number | Z coordinate. |
