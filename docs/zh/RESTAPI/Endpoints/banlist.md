# GET /banlist



**端点:** `GET /v1/pdapi/banlist`

**认证:** Bearer 令牌

**权限:** `REST.Banlist.Read`

## 用途

从封禁列表读取封禁记录。封禁相关数据存储在 `Banlist.json`，而不是 `Config.json`。

## 路径参数

无。

## 查询参数

- `active`: 使用 `true`、`false` 或 `1` 按有效状态筛选。
- `entryType`：按封禁条目类型过滤。
- `userId`: Filter by user ID.
- `ip` or `userIP`: Filter by IP address.
- `issuerType`、`issuerName`、`issuerIP`：按执行者元数据过滤。
- `reason`: 按原因文本筛选。
- `q`: 常规文本搜索。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/banlist.md"

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

## 示例

### 列出所有封禁记录

```http
GET /v1/pdapi/banlist
```

### 查找 Steam 用户的有效记录

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### 按 IP 搜索记录

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## 使用场景

- 检查玩家或 IP 当前是否被封禁。
- 解封前按原因或执行者搜索。
- 构建通过 API 读取 `Banlist.json` 的管理面板。

## Related

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), and [POST /unbanip](unbanip.md).
