# POST /give/paltemplate/{player_identifier}



**端点:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**认证:** Bearer 令牌

**权限:** `REST.PalTemplates.Give`

## 用途

从 `Pals/Templates/` 文件中给出一个或多个帕鲁。

## 路径参数

- `player_identifier`: 目标玩家的 `UserId` 或 `PlayerUID`。

## 查询参数

无。

## 请求体

JSON 对象，包含 `PalTemplates` 模板文件名数组。为了清晰起见，可以包含 `.json` 扩展名。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | 请求体不包含 `PalTemplates` 数组。 |
| `400` | `VALIDATION_FAILED` | One or more template filenames are invalid, cannot be imported, or do not fit in Pal storage. |

## 示例

### 向 Steam 玩家发放一个模板 Pal

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### 向 PS5 玩家发放 Raid 奖励模板

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## 使用场景

- 当奖励需要指定技能、被动、IV、souls、昵称或工作适应性数值时使用。
- 先使用 [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md) 创建模板。
- `Pals/ImportRules/` 中的导入规则可以在发放前阻止或调整模板。
