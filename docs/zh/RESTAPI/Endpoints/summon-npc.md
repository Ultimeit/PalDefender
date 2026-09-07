# POST /summon/npc

**端点：** `POST /v1/pdapi/summon/npc`  
**认证：** Bearer token  
**权限：** `REST.Summon.NPC`

## 用途

在固定地图坐标生成 NPC。

## 请求体

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `NPCID` | string | 是 | NPC ID 或 NPC Character ID。 |
| `X`, `Y`, `Z` | number | 是 | 地图坐标。 |
| `Level` | integer | 否 | NPC 等级（默认 `1`）。 |
| `Uncapturable` | bool | 否 | 禁止捕获（默认 `false`）。 |
| `DisableAI` | bool | 否 | 禁用普通 AI（默认 `false`）。 |

## 响应架构

--8<-- "_snippets/zh/restapi/schemas/summon-npc.md"

## 错误

除标准的认证/请求错误外，此路由还可能返回 `VALIDATION_FAILED` 或 `SUMMON_NPC_FAILED`。

## 示例

```http
POST /v1/pdapi/summon/npc
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "NPCID": "PIDF_Soldier_AssaultRifle",
    "Level": 30,
    "X": 230,
    "Y": -486,
    "Z": 4097
}
```
