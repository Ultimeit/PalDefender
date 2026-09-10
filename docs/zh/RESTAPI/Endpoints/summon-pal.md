# POST /summon/pal

**端点：** `POST /v1/pdapi/summon/pal`  
**认证：** Bearer token  
**权限：** `REST.Summon.Pal`

## 用途

在固定地图坐标生成 Pal。请求必须且只能提供 `PalID` 或 `PalTemplate` 其中之一。

## 请求体

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `PalID` | string | 二选一 | Pal 种类 ID。不能与 `PalTemplate` 同时使用。 |
| `PalTemplate` | string | 二选一 | `Pals/Templates/` 中的文件名；使用模板中的 Pal 和等级。 |
| `X`, `Y`, `Z` | number | 是 | 地图坐标。 |
| `Level` | integer | 否 | 使用 `PalID` 召唤时的等级（默认 `1`）。使用模板时忽略。 |
| `Uncapturable` | bool | 否 | 禁止捕获（默认 `false`）。 |
| `DisableAI` | bool | 否 | 禁用普通 AI（默认 `false`）。 |
| `DisableDamageMeter` | bool | 否 | 禁用伤害统计（默认 `false`）。 |
| `DisableStatuses` | array | 否 | 要禁用的状态名称。 |

!!! warning "最大生命值迁移"
    使用 `PalTemplate` 时，模板的 `HP` 值会成为生成帕鲁的最大生命值。请求不再接受 `HealthMultiplier` 和 `HPMultiplier`，响应也不再返回这些字段；请从现有 REST 集成中删除它们。

## 响应架构

--8<-- "_snippets/zh/restapi/schemas/summon-pal.md"

## 错误

除标准的 `INVALID_TOKEN`、`MISSING_PERMISSION`、`INVALID_JSON`、`REQUEST_FAILED` 和 `REQUEST_TIMEOUT` 响应外，此路由还可能返回 `VALIDATION_FAILED`、`PAL_TEMPLATE_IMPORT_FAILED` 或 `SUMMON_PAL_FAILED`。

## 示例

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true
}
```
