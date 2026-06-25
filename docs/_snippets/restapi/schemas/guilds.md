### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Guilds` | object[] | Known guild summaries. |

`Guilds[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `GuildId` | string | Guild identifier. |
| `Name` | string | Guild name. |
| `OwnerUserId` | string | User ID of the guild owner, when available. |
| `OwnerPlayerUID` | string | Player UID of the guild owner, when available. |
| `MemberCount` | integer | Number of known guild members. |
| `BaseCampCount` | integer | Number of known bases/camps owned by the guild. |
