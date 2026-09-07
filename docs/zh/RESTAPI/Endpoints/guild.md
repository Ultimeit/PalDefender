# GET /guild/{guild_id}



**端点:** `GET /v1/pdapi/guild/<guild_id>`

**认证:** Bearer 令牌

**权限:** `REST.Guild.Read`

## 用途

返回一个公会及其详细成员和基地/营地信息。

## 路径参数

- `guild_id`: 公会标识符，通常从 [GET /guilds](guilds.md) 复制。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` | 没有公会与提供的 `guild_id` 匹配。 |

## 示例

### 读取公会成员和基地

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### 按 GUID 读取另一个公会

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## 使用场景

- 删除基地前调查其所有权。
- 为支持请求查看公会成员和基地数据。
- 使用响应中的 Camp ID 调用 [POST /deletebase](deletebase.md) 时请谨慎。
