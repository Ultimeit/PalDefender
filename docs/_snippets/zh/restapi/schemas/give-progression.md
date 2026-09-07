### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Granted` | object | 此请求授予的进度值。 |
| `Totals` | object | 授予货币后更新的总数（如适用）。 |

`Granted` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `EXP` | integer | 请求时授予的经验值。 |
| `Relics` | object | 请求时按遗物类型授予的遗物点数。 |
| `TechnologyPoints` | integer | 请求时授予的科技点。 |
| `AncientTechnologyPoints` | integer | 请求时授予的古代科技点。 |

`Totals` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Relics` | object | 授予 `Relics` 后按类型更新的遗物点数总计。 |
| `TechnologyPoints` | integer | 授予 `TechnologyPoints` 后更新的科技点总计。 |
| `AncientTechnologyPoints` | integer | 授予 `AncientTechnologyPoints` 后更新的古代科技点总计。 |
