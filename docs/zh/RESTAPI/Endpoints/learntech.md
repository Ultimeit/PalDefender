# POST /learntech/{player_identifier}



**端点:** `POST /v1/pdapi/learntech/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Techs.Learn`

## 用途

Learns one, many, or all technologies for a player.

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

`Technology` can be a single [`TechID`](https://paldeck.cc/technology), the string `"All"`, or an array of [`TechID`](https://paldeck.cc/technology) strings. Do not put `"All"` inside an array.

## 响应结构

--8<-- "_snippets/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` is missing, or it is not a string/array in the expected format. |
| `400` | `VALIDATION_FAILED` | The `Technology` array contains a non-string, `All`, or an invalid technology identifier. |

## 示例

### Learn one technology for a Steam player

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Learn several technologies for a PS5 player

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Learn every technology by PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## 使用场景

- Unlock a missing recipe for support.
- Unlock all technologies for test accounts.
- Validate technology IDs at [paldeck.cc/technology](https://paldeck.cc/technology) before sending the request.
