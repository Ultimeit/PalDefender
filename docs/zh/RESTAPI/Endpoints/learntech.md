# POST /learntech/{player_identifier}



**端点:** `POST /v1/pdapi/learntech/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Techs.Learn`

## 用途

为玩家解锁一项、多项或全部科技。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

`Technology` 可以是单个 [`TechID`](https://paldeck.cc/technology)、字符串 `"All"`，或由 [`TechID`](https://paldeck.cc/technology) 字符串组成的数组。请勿将 `"All"` 放入数组中。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | 缺少 `Technology`，或它不是预期格式的字符串/数组。 |
| `400` | `VALIDATION_FAILED` | `Technology` 数组包含非字符串值、`All` 或无效的科技标识符。 |

## 示例

### 为 Steam 玩家解锁一个科技

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### 为 PS5 玩家解锁多个科技

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

### 按 PlayerUID 解锁全部科技

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## 使用场景

- 在支持处理中解锁缺少的配方。
- 为测试账户解锁全部科技。
- 发送请求前在 [paldeck.cc/technology](https://paldeck.cc/technology) 验证科技 ID。
