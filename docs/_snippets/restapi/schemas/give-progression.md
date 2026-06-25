### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Granted` | object | Progression values granted by the request. |
| `Totals` | object | Updated totals for granted currencies, when applicable. |

`Granted` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `EXP` | integer | EXP granted, when requested. |
| `Lifmunks` | integer | Lifmunk Effigy points granted, when requested. |
| `TechnologyPoints` | integer | Technology points granted, when requested. |
| `AncientTechnologyPoints` | integer | Ancient technology points granted, when requested. |

`Totals` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Lifmunks` | integer | Updated Lifmunk Effigy point total, when `Lifmunks` was granted. |
| `TechnologyPoints` | integer | Updated technology point total, when `TechnologyPoints` was granted. |
| `AncientTechnologyPoints` | integer | Updated ancient technology point total, when `AncientTechnologyPoints` was granted. |
