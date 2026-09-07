# POST /Broadcast



**端点:** `POST /v1/pdapi/Broadcast`

**认证:** Bearer 令牌

**权限:** `REST.Messages.Broadcast`

## 用途

向服务器广播聊天消息。

## 路径参数

无。

## 查询参数

无。

## 请求体

JSON 对象，包含必填字符串 `Message`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/broadcast.md"

## 错误响应

错误响应使用以下格式:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "人类可读的消息",
        "Details": {}
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
| `400` | `VALIDATION_FAILED` | `Message` 缺失、为空或不是字符串。 |

## 示例

### 广播重启提醒

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

## 使用场景

- 公告计划维护。
- 发送自动活动开始消息。
- 如果消息应作为警报而不是普通广播聊天发送，请使用 [POST /Alert](alert.md)。
