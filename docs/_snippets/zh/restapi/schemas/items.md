### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Meta` | object | 目标玩家元数据。 |
| `Inventory` | object | 目标玩家的库存容器。 |

`Meta` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `PlayerUID` | string | Palworld 存档数据使用的玩家 UID。 |
| `Player` | string | 请求路径中提供的玩家标识符。 |

`Inventory` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Items` | object | 普通库存容器。 |
| `KeyItems` | object | 关键物品库存容器。 |
| `Weapons` | object | 武器配置库存容器。 |
| `Armor` | object | 护甲库存容器。 |
| `Food` | object | 食物库存容器。 |
| `DropSlot` | object | 丢弃栏库存容器。 |

库存容器对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Available` | boolean | 容器是否可用。 |
| `ContainerID` | string | Palworld 容器 ID；不可用时为空字符串。 |
| `UsedSlots` | integer | 已占用栏位数。 |
| `MaxSlots` | integer | 栏位总数。 |
| `FreeSlots` | integer | 空闲栏位数。 |
| `Slots` | object | 以栏位索引为键的已占用栏位。 |

`Slots` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `ItemID` | string | Palworld 物品标识符。 |
| `Count` | integer | 栏位中的堆叠数量。 |
