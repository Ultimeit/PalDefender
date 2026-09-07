### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Success` | boolean | 成功记录 IP 封禁时为 `true`。 |
| `IP` | string | 被封禁的 IP 地址。 |
| `UserId` | string | 与 IP 封禁一同记录的可选用户 ID。 |
| `Kicked` | integer | 从该 IP 地址踢出的在线玩家数量。 |
