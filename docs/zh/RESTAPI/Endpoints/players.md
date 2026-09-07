# GET /players



**端点:** `GET /v1/pdapi/players`

**认证:** Bearer 令牌

**权限:** `REST.Players.Read`

## 用途

列出已知玩家及其标识和状态信息。可用于为管理员工具构建玩家选择器。

## 路径参数

无。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | 服务器无法访问 Palworld 玩家管理器。 |

## 示例

### 列出所有已知玩家

```http
GET /v1/pdapi/players
```

### 刷新管理员玩家选择器

```http
GET /v1/pdapi/players
```

## 使用场景

- 构建在线玩家和已知玩家的下拉列表。
- 调用奖励、处罚或库存端点前，先找到正确的 `UserId` 或 `PlayerUID`。
- 发送消息或计划维护警告前，审计当前在线玩家。

## Related

- 使用 [GET /player](player.md) 查询单个玩家。
- [POST /kick](kick.md)、[POST /ban](ban.md) 和奖励端点使用相同的玩家标识符格式。
