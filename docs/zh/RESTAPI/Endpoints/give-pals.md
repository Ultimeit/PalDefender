# POST /give/pals/{player_identifier}



**端点:** `POST /v1/pdapi/give/pals/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Pals.Give`

## 用途

按 ID 和等级发放一个或多个 Pals。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

JSON 对象，包含 `Pals` Pal 发放数组。每个条目都需要一个 [`PalID`](https://paldeck.cc/pals) 和正数 `Level`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` | 请求体不包含 `Pals` 数组。 |
| `400` | `VALIDATION_FAILED` | 一个或多个帕鲁发放项无效，或玩家的帕鲁存储空间不足。 |

## 示例

### 向 GDK 玩家发放初始 Pal

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### 按 PlayerUID 发放活动 Pals

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## 使用场景

- 在不维护模板文件的情况下发放简单 Pal 奖励。
- 用于只改变 `PalID` 和 `Level` 的随机奖励脚本。
- 如果找不到玩家、[`PalID`](https://paldeck.cc/pals) 无效，或 Pal 存储空间不足，请求可能失败。
