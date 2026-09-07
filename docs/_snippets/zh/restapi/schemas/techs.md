### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Meta` | object | 目标玩家的科技数量元数据。 |
| `Techs` | object | 目标玩家的科技数据。 |

`Meta` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `PlayerUID` | string | Palworld 存档数据使用的玩家 UID。 |
| `Player` | string | 请求路径中提供的玩家标识符。 |
| `UnlockedCount` | integer | 当前已解锁的科技数量。 |
| `LockedCount` | integer | 当前未解锁的科技数量。 |
| `TotalCount` | integer | 玩家数据已知的配方科技总数。 |

`Techs` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Unlocked` | string[] | 玩家当前已学习的科技 ID。 |
