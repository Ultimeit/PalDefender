### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Meta` | object | Technology count metadata for the target player. |
| `Techs` | object | Technology data for the target player. |

`Meta` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `PlayerUID` | string | Player UID used by Palworld save data. |
| `Player` | string | Player identifier supplied in the request path. |
| `UnlockedCount` | integer | Number of currently unlocked technologies. |
| `LockedCount` | integer | Number of currently locked technologies. |
| `TotalCount` | integer | Total number of recipe technologies known to the player data. |

`Techs` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Unlocked` | string[] | Technology IDs currently learned by the player. |
