# POST /Alert



**端点:** `POST /v1/pdapi/Alert`

**认证:** Bearer 令牌

**权限:** `REST.Messages.Alert`

## 用途

向服务器发送警报消息。

## 路径参数

无。

## 查询参数

无。

## 请求体

JSON 对象，包含字符串 `Message`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/alert.md"

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
| `400` | `BROADCAST_ALERT_FAILED` | 服务器发送警报消息失败。 |

## 示例

### 发送重启警报

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Restart now."
}
```

### 发送多行警报

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Server restart in 5 minutes.\nPlease return to base."
}
```

## 使用场景

- 发送高优先级服务器警告。
- 当玩家需要最后的紧急提醒时，可在广播后使用。
- 保持警报简短，方便在游戏内阅读。
