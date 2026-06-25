### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Meta` | object | Guild list metadata. |
| `Guilds` | object | Known guild summaries keyed by guild UUID. |

`Meta` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `GuildCount` | integer | Number of guilds returned. |

Guild summary object schema:

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | Guild name. |
| `Level` | integer | Guild base camp level. |
| `admin` | object | Guild admin details. |
| `camp_count` | integer | Number of base camps in the guild. |
| `camps` | object[] | Base camp summaries. |
| `member_count` | integer | Number of guild members. |
| `members` | string[] | Guild member PlayerUID values. |

`admin` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Admin PlayerUID. |
| `name` | string | Admin player name. |

`camps[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Base camp GUID. |
| `world_pos` | object | Base camp world coordinates. |
| `map_pos` | object | Converted map coordinates. |

Coordinate object schema:

| Field | Type | Description |
|-------|------|-------------|
| `x` | number | X coordinate. |
| `y` | number | Y coordinate. |
| `z` | number | Z coordinate. |
