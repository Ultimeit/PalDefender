# POST /give/items/{player_identifier}



**端点:** `POST /v1/pdapi/give/items/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Items.Give`

## 用途

给目标玩家一个或多个物品。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

JSON 对象，包含 `Items` 物品发放数组。每个条目都需要一个 [`ItemID`](https://paldeck.cc/items) 和正数 `Count`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` | 请求体不包含 `Items` 数组。 |
| `400` | `VALIDATION_FAILED` | One or more item grants are invalid, unsupported, too large, or do not fit in inventory. |
| `500` | `GRANT_FAILED` | 验证通过，但服务器向库存添加物品时失败。 |

## 示例

### 向 Steam 玩家发放弹药和发射器

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### 向 PS5 玩家发放货币

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## 使用场景

- 用于回档后的补偿礼包。
- 用于可信服务发放已购买物品的商店集成。
- 首先验证 [`ItemID`](https://paldeck.cc/items)；显示名称不一定是有效 ID。
