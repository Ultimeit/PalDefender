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

--8<-- "_snippets/restapi/schemas/unban.md"

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
| `404` | `BAN_NOT_FOUND` | 提供的 `user_id` 当前未被封禁。 |

## 示例

### Unban a Steam user

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### Unban a PS5 user with default reason

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## 使用场景

- Remove a user ban after appeal approval.
- Keep a reason for the audit trail.
- 使用带 `userId` 或 `q` 的 [GET /banlist](banlist.md) 验证结果。
