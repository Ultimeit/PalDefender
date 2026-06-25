### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Meta` | object | Target player metadata. |
| `Inventory` | object | Inventory containers for the target player. |

`Meta` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `PlayerUID` | string | Player UID used by Palworld save data. |
| `Player` | string | Player identifier supplied in the request path. |

`Inventory` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Items` | object | Common inventory container. |
| `KeyItems` | object | Key item inventory container. |
| `Weapons` | object | Weapon loadout inventory container. |
| `Armor` | object | Armor inventory container. |
| `Food` | object | Food inventory container. |
| `DropSlot` | object | Drop slot inventory container. |

Inventory container object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Available` | boolean | Whether the container was available. |
| `ContainerID` | string | Palworld container ID, or an empty string when unavailable. |
| `UsedSlots` | integer | Number of occupied slots. |
| `MaxSlots` | integer | Total slot count. |
| `FreeSlots` | integer | Number of free slots. |
| `Slots` | object | Occupied slots keyed by slot index. |

`Slots` item schema:

| Field | Type | Description |
|-------|------|-------------|
| `ItemID` | string | Palworld item identifier. |
| `Count` | integer | Stack count in the slot. |
