# POST /give/paleggs/{player_identifier}



**端点:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.PalEggs.Give`

## 用途

向目标玩家发放一个或多个 Pal 蛋。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

JSON 对象，包含 `PalEggs` 蛋发放数组。`EggID` 是一个 [`ItemID`](https://paldeck.cc/items)。每个蛋必须使用 [`PalID`](https://paldeck.cc/pals) 或 `PalTemplate`，不能同时使用两者。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | 请求体不包含 `PalEggs` 数组。 |
| `400` | `VALIDATION_FAILED` | One or more egg grants are invalid, cannot be imported, or do not fit in inventory. |

## 示例

### 向 Steam 玩家发放带等级的蛋

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### 按 PlayerUID 发放基于模板的蛋

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## 使用场景

- 发放活动蛋，而不立即生成 Pal。
- 简单蛋使用 `PalID`，自定义蛋内容使用 `PalTemplate`。
- 如果蛋的 [`ItemID`](https://paldeck.cc/items) 无效或玩家背包没有空间，请求可能失败。
