# GET /items/{player_identifier}



**端点:** `GET /v1/pdapi/items/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Items.Read`

## 用途

列出目标玩家的物品。响应中的物品标识可在 [paldeck.cc/items](https://paldeck.cc/items) 查询。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` | 无法解析目标玩家、玩家状态、背包数据或通用背包容器。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |

## 示例

### Read inventory for a Steam player

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### Read inventory for a GDK player

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## 使用场景

- Check inventory before giving compensation.
- Confirm an [`ItemID`](https://paldeck.cc/items) before using [POST /give/items](give-items.md).
- Troubleshoot reports about missing items.
