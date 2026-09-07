### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Meta` | object | 玩家列表计数。 |
| `Players` | object[] | 包含标识、公会、状态和位置信息的已知玩家。 |

`Meta` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `PlayerCount` | integer | 返回的玩家账户数量。 |
| `OnlineCount` | integer | 返回结果中当前在线的玩家数量。 |

`Players[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Name` | string | 当前或已保存的玩家名称。 |
| `IP` | string | 玩家 IP 地址；不可用时为空字符串。 |
| `PlayerUID` | string | Palworld 存档数据使用的玩家 UID。 |
| `UserId` | string | 平台用户 ID；不可用时为空字符串。 |
| `GuildName` | string | 公会名称；不可用时为空字符串。 |
| `GuildUUID` | string | 公会 UUID；不可用时为零 GUID。 |
| `Status` | string | 已保存的玩家账户状态。 |
| `WorldLocation` | object | 当前或最后保存的世界坐标。 |
| `MapLocation` | object | 转换后的地图坐标。 |

位置对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `x` | number | X 坐标。 |
| `y` | number | Y 坐标。 |
| `z` | number | Z 坐标。 |
