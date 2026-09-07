# POST /unban/{user_id}



**端点:** `POST /v1/pdapi/unban/<user_id>`

**认证:** Bearer 令牌

**权限:** `REST.Punishments.Unban`

## 用途

Unbans a user ID in `Banlist.json`.

## 路径参数

- `user_id`: User ID to unban.

## 查询参数

无。

## 请求体

可选 JSON 字段：字符串 `Reason`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/unban.md"

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
| `400` | `VALIDATION_FAILED` | 可选请求字段的 JSON 类型错误。 |
| `404` | `BAN_NOT_FOUND` | 提供的 `user_id` 当前未被封禁。 |

## 示例

### 解封 Steam 用户

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### 使用默认原因解封 PS5 用户

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## 使用场景

- 申诉获准后解除用户封禁。
- 保留原因以供审计追踪。
- 使用带 `userId` 或 `q` 的 [GET /banlist](banlist.md) 验证结果。
