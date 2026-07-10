# GET /progression/{player_identifier}



**端点:** `GET /v1/pdapi/progression/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Progression.Read`

## 用途

读取玩家进度值，例如 EXP、等级相关状态、遗物总数和科技点总数。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/progression.md"

## 错误响应

错误响应使用以下格式:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "人类可读的消息",
        "详情": {}
    }
}
```

| HTTP | 错误代码 | 发生条件 |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` 头缺失、格式错误，或与配置的 Bearer 令牌不匹配。 |
| `403` | `MISSING_PERMISSION` | 令牌有效，但不包含此端点权限。 |
| `400` | `INVALID_JSON` | 提供了请求体，但无法解析为 JSON。 |
| `400` | `REQUEST_FAILED` | 无法解析目标玩家、账号、个人角色数据、记录数据或科技数据。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |

## 示例

### Read progression by PS5 UserID

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### Read progression by PlayerUID

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## 使用场景

- Confirm the current values before granting progression.
- Verify a support action after [POST /give/progression](give-progression.md).
- Build a player overview panel in a trusted admin dashboard.
