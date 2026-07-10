# GET /guilds



**端点:** `GET /v1/pdapi/guilds`

**认证:** Bearer 令牌

**权限:** `REST.Guilds.Read`

## 用途

列出已知公会及摘要信息。请求特定公会前可使用此端点查找公会 ID。

## 路径参数

无。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/guilds.md"

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

## 示例

### List all guilds

```http
GET /v1/pdapi/guilds
```

### Refresh guild dashboard data

```http
GET /v1/pdapi/guilds
```

## 使用场景

- Build a guild selector in an admin panel.
- Find the `guild_id` for [GET /guild](guild.md).
- Audit base counts, member counts, and guild ownership at a glance.
