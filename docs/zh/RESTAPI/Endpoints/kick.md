# POST /kick/{player_identifier}



**端点:** `POST /v1/pdapi/kick/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Punishments.Kick`

## 用途

踢出在线玩家，但不创建封禁记录。

## 路径参数

- `player_identifier`: `UserId`、`PlayerUID` 或其他受支持的玩家标识符。

## 查询参数

无。

## 请求体

可选 JSON 字段：字符串 `Reason`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` | 目标玩家不在线或无法找到。 |

## 示例

### 踢出 GDK 玩家并提供原因

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "AFK in event area"
}
```

### 使用默认原因踢出 Steam 玩家

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## 使用场景

- 在维护前移除玩家。
- 踢出卡住的玩家，使其可以重新连接。
- 如果不应允许玩家返回，请改用 [POST /ban](ban.md)。
