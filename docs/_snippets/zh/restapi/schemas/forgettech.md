### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `ForgottenCount` | integer | 从玩家移除的科技数量。 |
| `Forgotten` | string[] 或 string | 已移除的科技 ID；移除全部已解锁科技时为 `All`。 |
| `Skipped` | string[] | 因尚未解锁而跳过的科技 ID。 |
