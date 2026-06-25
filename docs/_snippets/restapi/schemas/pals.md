### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Pals` | object[] | Pals owned by the target player. |

`Pals[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `PalID` | string | Pal identifier. |
| `Nickname` | string | Custom Pal name, when available. |
| `Level` | integer | Current Pal level. |
| `CharacterID` | string | Internal Pal character identifier, when available. |
| `Gender` | string | Pal gender, when available. |
| `IsBoss` | boolean | Whether the Pal is a boss variant. |
| `IsLucky` | boolean | Whether the Pal is a lucky variant. |
