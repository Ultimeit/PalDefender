# GET /player/{player_identifier}



**端点:** `GET /v1/pdapi/player/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Player.Read`

## 用途

返回一个玩家。标识符可以是支持的玩家标识，例如 `UserId` 或 `PlayerUID`。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/player.md"

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
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | 已找到玩家，但无法加载玩家账号数据。 |

## 示例

### Lookup by Steam UserID

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### Lookup by PlayerUID

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## 使用场景

- 从 `GET /players` 选择一行后，打开玩家详情页。
- Confirm the target before giving rewards or applying punishments.
- Check whether the player can currently be resolved by the server.
