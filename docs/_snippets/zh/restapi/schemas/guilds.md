### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Meta` | object | 公会列表元数据。 |
| `Guilds` | object | 以公会 UUID 为键的已知公会摘要。 |

`Meta` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `GuildCount` | integer | 返回的公会数量。 |

公会摘要对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `name` | string | 公会名称。 |
| `Level` | integer | 公会基地等级。 |
| `admin` | object | 公会管理员详情。 |
| `camp_count` | integer | 公会中的基地数量。 |
| `camps` | object[] | 基地摘要。 |
| `member_count` | integer | 公会成员数量。 |
| `members` | string[] | 公会成员的 PlayerUID 值。 |

`admin` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `id` | string | 管理员 PlayerUID。 |
| `name` | string | 管理员玩家名称。 |

`camps[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `id` | string | 基地 GUID。 |
| `world_pos` | object | 基地世界坐标。 |
| `map_pos` | object | 转换后的地图坐标。 |

坐标对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `x` | number | X 坐标。 |
| `y` | number | Y 坐标。 |
| `z` | number | Z 坐标。 |
