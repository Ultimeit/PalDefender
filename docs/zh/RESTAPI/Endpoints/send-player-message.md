# POST /SendPlayerMessage



**端点:** `POST /v1/pdapi/SendPlayerMessage`

**认证:** Bearer 令牌

**权限:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## 用途

向一个或多个目标玩家发送消息。

## 路径参数

无。

## 查询参数

无。

## 请求体

JSON 对象，包含 `SendType`、`Message`，以及 `UserID` 或 `UserIDs`。常见 `SendType` 值包括 `PlayerChat`、`PlayerGlobalChat`、`PlayerGuildChat`、`PlayerLogNormal`、`PlayerLogImportant` 和 `PlayerLogVeryImportant`。

## 响应结构

--8<-- "_snippets/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` | 请求体为空。 |
| `400` | `INVALID_JSON` | 请求体不是有效 JSON。 |
| `400` | `VALIDATION_FAILED` | `SendType`、`Message`、`UserID` 或 `UserIDs` 缺失、为空、重复，或类型错误。 |
| `400` | `PLAYER_NOT_FOUND` | One or more target user IDs or player UIDs could not be found. |
| `400` | `SEND_MESSAGE_FAILED` | Validation passed, but the server rejected the message send operation. |
| `400` | `REQUEST_FAILED` | 游戏线程回调抛出异常。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |

## 示例

### 向单个用户发送玩家聊天

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived."
}
```

### 向多个类型目标发送重要日志

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "活动将在 10 分钟后开始。"
}
```

## 使用场景

- 向选定玩家发送直接重启警告。
- 从管理员面板发送支持回复。
- 单个目标使用 `UserID`，多个目标使用 `UserIDs`，不要同时使用。
