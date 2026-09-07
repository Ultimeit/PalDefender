### 200 response schema

| Field | Type | Description |
| --- | --- | --- |
| `Summoned` | object | Details of the spawned Pal. |

`Summoned` contains `Type` (`"Pal"`), `PalID`, `Level`, `Uncapturable`, `DisableAI`, `HealthMultiplier`, `DamageMeter`, and the requested `X`, `Y`, and `Z`. `PalTemplate` is also returned when a template was used.
