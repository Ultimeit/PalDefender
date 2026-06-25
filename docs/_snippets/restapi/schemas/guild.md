### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `GuildId` | string | Guild identifier. |
| `Name` | string | Guild name. |
| `OwnerUserId` | string | User ID of the guild owner, when available. |
| `OwnerPlayerUID` | string | Player UID of the guild owner, when available. |
| `MemberCount` | integer | Number of known guild members. |
| `BaseCampCount` | integer | Number of known bases/camps owned by the guild. |
| `Members` | object[] | Detailed guild member records. |
| `BaseCamps` | object[] | Detailed base/camp records. |

`Members[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `Name` | string | Player name. |
| `UserId` | string | Player user ID. |
| `PlayerUID` | string | Player UID. |
| `IsOnline` | boolean | Whether the member is currently online. |

`BaseCamps[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `BaseCampId` | string | Base camp identifier. |
| `Name` | string | Base/camp name, when available. |
| `LocationX` | number | Base location X coordinate. |
| `LocationY` | number | Base location Y coordinate. |
| `LocationZ` | number | Base location Z coordinate. |
