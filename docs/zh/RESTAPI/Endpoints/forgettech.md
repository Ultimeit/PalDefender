# POST /forgettech/{player_identifier}



**端点:** `POST /v1/pdapi/forgettech/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Techs.Forget`

## 用途

移除玩家的一项、多项或全部科技。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

`Technology` 可以是单个 [`TechID`](https://paldeck.cc/technology)、字符串 `"All"`，或由 [`TechID`](https://paldeck.cc/technology) 字符串组成的数组。请勿将 `"All"` 放入数组中。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/forgettech.md"

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

### 移除 GDK 玩家的一个科技

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### 按 PlayerUID 移除多个科技

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### 移除 Steam 玩家的全部科技

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## 使用场景

- 移除误授予的科技。
- 使用 `"All"` 重置测试账户。
- 在请求前后使用 [GET /techs](techs.md) 确认当前状态。
