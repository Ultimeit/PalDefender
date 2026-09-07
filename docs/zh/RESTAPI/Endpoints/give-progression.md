# POST /give/progression/{player_identifier}



**端点:** `POST /v1/pdapi/give/progression/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.Progression.Give`

## 用途

给玩家授予进度数值。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

JSON 对象，至少包含一种支持的授予内容：正整数 `EXP`、正整数 `TechnologyPoints`、正整数 `AncientTechnologyPoints`，或非空对象 `Relics`，其中键为遗物类型，值为正整数数量。


支持的遗物类型: `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/give-progression.md"

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
| `400` | `INVALID_REQUEST` | 请求体未包含 `EXP`、`Relics`、`TechnologyPoints` 或 `AncientTechnologyPoints` 中的任何字段。 |
| `400` | `VALIDATION_FAILED` | 提供的进度值缺失、不是整数、不是正数，或所需的内部进度数据不可用。 |

## 示例

### 给 GDK 玩家经验值

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### 通过 PlayerUID 给予点数和遗物

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## 使用场景

- 在存档回滚后补偿玩家。
- 添加科技点而不解锁特定科技。
- 如果要解锁特定 [`TechID`](https://paldeck.cc/technology)，请改用 [POST /learntech](learntech.md)。
