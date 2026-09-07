### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `BaseCamp` | object | 已删除基地的摘要。 |
| `Deleted` | object | 已删除基地数据的清理计数。 |
| `Archive` | string | 已生成审计归档的路径。 |

`BaseCamp` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Id` | string | 基地 GUID。 |
| `Summary` | string | 便于阅读的基地摘要。 |

`Deleted` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `BaseCampPals` | integer | 已删除的基地帕鲁数量。 |
| `StorageContainers` | integer | 已清空的储物容器数量。 |
| `ItemStacks` | integer | 已删除的物品堆数量。 |
| `ItemCount` | integer | 已删除的物品总数。 |
| `Buildings` | integer | 已删除的建筑数量。 |
| `DropItems` | integer | 已删除的掉落物品 Actor 数量。 |
| `DefenseModels` | integer | 已删除的防御模型数量。 |
| `OtherMapObjects` | integer | 已删除的其他地图对象数量。 |
| `PalBox` | boolean | 是否删除了基地终端。 |
