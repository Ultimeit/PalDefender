# GET /techs/{player_identifier}



**端点:** `GET /v1/pdapi/techs/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Techs.Read`

## 用途

列出玩家的科技信息。科技标识符可在 [paldeck.cc/technology](https://paldeck.cc/technology) 查询。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | 无法解析目标玩家、玩家账号、科技数据或科技表。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |

## 示例

### Read unlocked techs by UserID

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### Read unlocked techs by PlayerUID

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## 使用场景

- Check whether a player already has a [`TechID`](https://paldeck.cc/technology) before learning or forgetting it.
- Build an admin page that separates unlocked and available technologies.
- Audit progression after support actions.
