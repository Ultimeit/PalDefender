# GET /pals/{player_identifier}



**端点:** `GET /v1/pdapi/pals/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Pals.Read`

## 用途

列出目标玩家的帕鲁。响应中的帕鲁标识可在 [paldeck.cc/pals](https://paldeck.cc/pals) 查询。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/pals.md"

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
| `400` | `REQUEST_FAILED` | 游戏线程回调抛出异常，或共享玩家/资源解析器失败。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |
| `404` | `PLAYER_NOT_FOUND` | No online player matched the supplied `player_identifier`. |
| `404` | `PLAYER_STATE_NOT_FOUND` | 玩家存在，但其 `APalPlayerState` 不可用。 |

## 示例

### Read Pals for a PS5 player

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### Read Pals by PlayerUID

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## 使用场景

- Review a player before support actions.
- Confirm that a reward Pal arrived after using [POST /give/pals](give-pals.md) or [POST /give/paltemplate](give-paltemplate.md).
- Investigate reports about missing or unexpected Pals.
