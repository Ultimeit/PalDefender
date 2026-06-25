### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Players` | object[] | Known players with identifying and status information. |

`Players[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `Name` | string | Player name. |
| `AccountName` | string | Platform account name. |
| `PlayerId` | string | Palworld player ID. |
| `UserId` | string | Platform user ID. |
| `PlayerUID` | string | Player UID used by Palworld save data. |
| `IP` | string | Player IP address, when available. |
| `Ping` | number | Current player ping, when available. |
| `LocationX` | number | Player location X coordinate, when available. |
| `LocationY` | number | Player location Y coordinate, when available. |
| `Level` | integer | Current player level. |
| `BuildingCount` | integer | Number of buildings owned by the player. |
| `IsOnline` | boolean | Whether the player is currently online. |
