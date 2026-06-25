### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Meta` | object | Target player metadata. |
| `Progression` | object | Progression, currency, defeat, capture, and activity data. |

`Meta` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `PlayerUID` | string | Player UID used by Palworld save data. |
| `Player` | string | Player identifier supplied in the request path. |

`Progression` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Player` | object | Player level, EXP, and unused status points. |
| `Currencies` | object | Lifmunk and technology point totals. |
| `Bosses` | object | Boss defeat counters and flags. |
| `Captures` | object | Pal capture and butcher counters. |
| `Activities` | object | Crafting, dungeon, fishing, treasure, and other activity counters. |

`Progression.Player` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `level` | integer | Current player level. |
| `exp` | integer | Current EXP value. |
| `unusedStatusPoints` | integer | Unused player status points. |

`Progression.Currencies` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `lifmunks` | integer | Lifmunk Effigy point total. |
| `technologyPoints` | integer | Technology point total. |
| `ancientTechnologyPoints` | integer | Ancient technology point total. |

`Progression.Bosses` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `towerBossDefeatCounts` | object | Tower boss defeat counts keyed by boss ID. |
| `normalBossDefeatFlags` | object | Normal boss defeat flags keyed by boss ID. |
| `raidBossDefeatCounts` | object | Raid boss defeat counts keyed by boss ID. |
| `totalBossDefeatCount` | integer | Sum of tower boss defeat counts. |
| `predatorDefeatCount` | integer | Predator defeat count. |

`Progression.Captures` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `tribeCaptureCount` | integer | Total tribe capture count. |
| `palCaptureCounts` | object | Pal capture counts keyed by Pal ID. |
| `palCaptureBonusCounts` | object | Pal capture bonus counts keyed by Pal ID. |
| `palButcherCounts` | object | Pal butcher counts keyed by Pal ID. |

`Progression.Activities` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `craftItemCounts` | object | Crafted item counts keyed by item ID. |
| `normalDungeonClearCount` | integer | Normal dungeon clear count. |
| `fixedDungeonClearCount` | integer | Fixed dungeon clear count. |
| `oilrigClearCount` | integer | Oil rig clear count. |
| `palRankUpCounts` | object | Pal rank-up counts keyed by Pal ID. |
| `arenaSoloClearCounts` | object | Arena solo clear counts keyed by arena ID. |
| `npcTalkCounts` | object | NPC talk counts keyed by NPC ID. |
| `fishingCounts` | object | Fishing counts keyed by fish ID. |
| `foundTreasureCount` | integer | Found treasure count. |
| `campConqueredCount` | integer | Camp conquered count. |
| `firstFishingComplete` | boolean | Whether first fishing completion is recorded. |
