# POST /ban/{player_identifier}



**端点:** `POST /v1/pdapi/ban/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Punishments.Ban`

## 用途

封禁用户并将记录写入 `Banlist.json`。如果目标当前在线，可能会被踢出。

## 路径参数

- `player_identifier`: `UserId`, `PlayerUID`, or another supported player identifier.

## 查询参数

无。

## 请求体

可选 JSON 字段：字符串 `Reason` 和布尔值 `IP`。只有在同时想封禁解析出的 IP 地址时，才将 `IP` 设为 `true`。

## 响应结构

--8<-- "_snippets/restapi/schemas/ban.md"

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
| `400` | `VALIDATION_FAILED` | An optional request field has the wrong JSON type. |
| `400` | `IP_UNAVAILABLE` | `IP` was `true`, but the server could not resolve an IP for the target user. |

## 示例

### Ban a Steam user

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Chargeback fraud"
}
```

### Ban a PS5 user and their resolved IP

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Ban evasion",
    "IP": true
}
```

## 使用场景

- Ban a player by `UserId` after moderation review.
- Include a clear reason so future staff can understand the banlist entry.
- 使用 [GET /banlist](banlist.md) 验证活动记录。封禁相关数据不再由 `Config.json` 管理。
