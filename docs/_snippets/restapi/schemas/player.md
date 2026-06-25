### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Player` | object | Player details. |

`Player` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Name` | string | Current or saved player name. |
| `IP` | string | Player IP address, or an empty string when unavailable. |
| `PlayerUID` | string | Player UID used by Palworld save data. |
| `UserId` | string | Platform user ID, or an empty string when unavailable. |
| `GuildName` | string | Guild name, or an empty string when unavailable. |
| `GuildUUID` | string | Guild UUID, or a zero GUID when unavailable. |
| `Status` | string | Saved player account state. |
| `WorldLocation` | object | Current or last saved world coordinates. |
| `MapLocation` | object | Converted map coordinates. |

Location object schema:

| Field | Type | Description |
|-------|------|-------------|
| `x` | number | X coordinate. |
| `y` | number | Y coordinate. |
| `z` | number | Z coordinate. |
