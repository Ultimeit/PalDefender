### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Banlist` | object | 应用查询筛选条件后的封禁列表数据。 |

`Banlist` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Version` | integer | 封禁列表文件格式版本。 |
| `BannedMessage` | string | 向被封禁玩家显示的消息。 |
| `UserEntries` | object[] | 符合指定筛选条件的用户封禁条目。 |
| `IPEntries` | object[] | 符合指定筛选条件的 IP 封禁条目。 |

`UserEntries[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `UserId` | string | 被封禁的用户 ID。 |
| `Active` | boolean | 此封禁当前是否有效。 |
| `BannedBy` | object | 执行封禁操作的来源数据。 |
| `UnbannedBy` | object | 执行解封操作的来源数据（如果存在）。 |

`IPEntries[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `IP` | string | 被封禁的 IP 地址。 |
| `Active` | boolean | 此封禁当前是否有效。 |
| `BannedBy` | object | 执行封禁操作的来源数据。 |
| `UnbannedBy` | object | 执行解封操作的来源数据（如果存在）。 |

操作来源对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Type` | string | 来源类型，例如 `rest`、`player` 或 `system`。 |
| `NameValue` | string | 来源名称、用户 ID、令牌，或作为后备值的来源类型。 |
| `IP` | string | 来源 IP 地址元数据。 |
| `Reason` | string | 为此操作记录的原因。 |
| `Timestamp` | object | 此操作的 UTC 时间戳组成部分。 |

时间戳对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `UTC` | integer | 以秒为单位的 Unix 时间戳。 |
| `Year` | integer | UTC 年份。 |
| `Month` | integer | UTC 月份。 |
| `Day` | integer | UTC 月中日期。 |
| `Hour` | integer | UTC 小时。 |
| `Min` | integer | UTC 分钟。 |
| `Sec` | integer | UTC 秒。 |
| `Msec` | integer | 毫秒部分。 |
