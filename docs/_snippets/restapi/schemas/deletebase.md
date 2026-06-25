### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `BaseCamp` | object | Deleted base camp summary. |
| `Deleted` | object | Cleanup counts for deleted base camp data. |
| `Archive` | string | Path to the generated audit archive. |

`BaseCamp` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `Id` | string | Base camp GUID. |
| `Summary` | string | Human-readable base camp summary. |

`Deleted` object schema:

| Field | Type | Description |
|-------|------|-------------|
| `BaseCampPals` | integer | Number of base camp Pals deleted. |
| `StorageContainers` | integer | Number of storage containers cleared. |
| `ItemStacks` | integer | Number of item stacks deleted. |
| `ItemCount` | integer | Total item count deleted. |
| `Buildings` | integer | Number of buildings deleted. |
| `DropItems` | integer | Number of dropped item actors deleted. |
| `DefenseModels` | integer | Number of defense models deleted. |
| `OtherMapObjects` | integer | Number of other map objects deleted. |
| `PalBox` | boolean | Whether the base Palbox was deleted. |
