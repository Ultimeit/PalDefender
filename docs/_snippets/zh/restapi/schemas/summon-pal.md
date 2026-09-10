### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Summoned` | object | 已生成帕鲁的详细信息。 |

`Summoned` 包含 `Type`（`"Pal"`）、`PalID`、`Level`、`Uncapturable`、`DisableAI`、`DamageMeter`，以及请求中的 `X`、`Y` 和 `Z`。使用模板时还会返回 `PalTemplate`。
