# POST /unbanip/{ip}



**端点:** `POST /v1/pdapi/unbanip/<ip>`

**认证:** Bearer 令牌

**权限:** `REST.Punishments.UnbanIP`

## 用途

Unbans an IP address in `Banlist.json`.

## 路径参数

- `ip`: IP address to unban.

## 查询参数

无。

## 请求体

可选 JSON 字段：字符串 `Reason`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/unbanip.md"

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
| `404` | `BAN_NOT_FOUND` | 提供的 `ip` 当前未被封禁。 |

## 示例

### 提供原因并解除 IP 封禁

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Temporary block expired"
}
```

### 使用默认原因解除 IP 封禁

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## 使用场景

- 调查后解除 IP 封禁。
- 当玩家解除账号封禁后仍被阻止，且原因是 IP 记录仍处于活动状态时使用。
- 使用带 `ip` 的 [GET /banlist](banlist.md) 验证结果。
