### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Success` | boolean | 成功记录封禁时为 `true`。 |
| `UserId` | string | 被封禁的用户 ID。 |
| `IP` | boolean | 请求是否同时封禁了 IP 地址。 |
| `BannedIP` | string | 被封禁的 IP 地址；未封禁 IP 时为空字符串。 |
| `Kicked` | integer | 此封禁操作踢出的在线玩家数量。 |
