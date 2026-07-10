### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Granted` | object | Progression values granted by the request. |
| `Totals` | object | Updated totals for granted currencies, when applicable. |

`Granted` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `EXP` | integer | EXP granted, when requested. |
| `Relics` | object | Relic point amounts granted by relic type, when requested. |
| `TechnologyPoints` | integer | Technology points granted, when requested. |
| `AncientTechnologyPoints` | integer | Ancient technology points granted, when requested. |

`Totals` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Relics` | object | Updated relic point totals by relic type, when `Relics` was granted. |
| `TechnologyPoints` | integer | Updated technology point total, when `TechnologyPoints` was granted. |
| `AncientTechnologyPoints` | integer | Updated ancient technology point total, when `AncientTechnologyPoints` was granted. |
