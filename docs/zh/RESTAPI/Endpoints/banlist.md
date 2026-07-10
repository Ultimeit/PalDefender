# GET /banlist



**端点:** `GET /v1/pdapi/banlist`

**认证:** Bearer 令牌

**权限:** `REST.Banlist.Read`

## 用途

从封禁列表读取封禁记录。封禁相关数据存储在 `Banlist.json`，而不是 `Config.json`。

## 路径参数

无。

## 查询参数

- `active`: `true`, `false`, or `1` to filter active state.
- `entryType`：按封禁条目类型过滤。
- `userId`: Filter by user ID.
- `ip` or `userIP`: Filter by IP address.
- `issuerType`、`issuerName`、`issuerIP`：按执行者元数据过滤。
- `reason`: Filter by reason text.
- `q`: General text search.

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/banlist.md"

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

## 示例

### List all ban records

```http
GET /v1/pdapi/banlist
```

### Find active records for a Steam user

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### Search records by IP

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## 使用场景

- Check whether a player or IP is currently banned.
- Search by reason or issuer before unbanning.
- Build a moderation dashboard that reads from `Banlist.json` through the API.

## Related

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), and [POST /unbanip](unbanip.md).
