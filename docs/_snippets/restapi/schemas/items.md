### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Items` | object[] | Items found for the target player. |

`Items[]` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `ItemID` | string | Palworld item identifier. |
| `Count` | integer | Item stack count. |
| `SlotIndex` | integer | Inventory slot index, when available. |
| `Container` | string | Inventory container or category, when available. |
