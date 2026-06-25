### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Guild` | object | Guild details. |

`Guild` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Guild name. |
| `Level` | integer | Guild base camp level. |
| `admin` | object | Guild admin details. |
| `member_count` | integer | Number of guild members. |
| `members` | object[] | Detailed guild member records. |
| `camp_count` | integer | Number of base camps in the guild. |
| `camps` | object[] | Detailed base camp records. |
| `items` | object | Guild item storage data. |
| `expeditions` | object | Guild expedition data. |
| `laboratory` | object | Guild laboratory research data. |

`admin` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Admin PlayerUID. |
| `name` | string | Admin player name. |

`members[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `player_uid` | string | Member PlayerUID. |
| `player_name` | string | Member player name. |
| `status` | string | Member status. |

`camps[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Base camp GUID. |
| `level` | integer | Base camp level. |
| `world_pos` | object | Base camp world coordinates. |
| `map_pos` | object | Converted map coordinates. |
| `state` | string | Current base camp state. |
| `pals` | object | Base camp worker Pals keyed by Pal instance ID. |
| `buildings` | string | Current building payload placeholder. |

Coordinate object schema:

| Field | Type | Description |
|-------|------|-------------|
| `x` | number | X coordinate. |
| `y` | number | Y coordinate. |
| `z` | number | Z coordinate. |

Camp Pal object schema:

| Field | Type | Description |
|-------|------|-------------|
| `nickname` | string | Pal nickname. |
| `pal_id` | string | Pal species identifier. |
| `npc_id` | string | Unique NPC ID. |
| `skin_id` | string | Skin ID. |
| `gender` | string | Pal gender. |
| `level` | integer | Pal level. |
| `shiny` | boolean | Whether this is a rare Pal. |
| `phisical_health` | string | Physical health state as returned by the current API. |
| `worker_sick` | string | Worker sickness state. |
| `san` | number | Sanity value. |
| `imported` | boolean | Whether this is marked as imported. |
| `friendship` | integer | Friendship point value. |
| `active_skills` | string[] | Equipped active skills. |
| `learnt_skills` | string[] | Learned skills. |
| `passives` | string[] | Passive skill IDs. |

`items` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `container_id` | string | Guild item container ID, when available. |
| `current` | integer | Number of occupied slots. |
| `max` | integer | Total slot count. |
| `<slot_index>` | object | Slot item object keyed by numeric slot index. |

Guild item slot object schema:

| Field | Type | Description |
|-------|------|-------------|
| `item_id` | string | Item ID in the slot. |
| `count` | integer | Stack count in the slot. |

`expeditions` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `finished` | integer | Finished expedition count. |
| `missions` | object | Released mission flags keyed by mission ID. |

`laboratory` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `current_research` | string | Current research ID. |
| `researches` | object | Active research progress keyed by research ID. |

Research progress object schema:

| Field | Type | Description |
|-------|------|-------------|
| `work_amount` | number | Current work amount. |
| `required_work_amount` | number | Required work amount. |
| `percentage` | number | Current work divided by required work. |
