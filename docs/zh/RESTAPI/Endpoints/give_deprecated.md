# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>已废弃</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>已废弃</span> legacy endpoint"
    此旧版奖励端点已废弃。建议改用拆分后的奖励端点：[give progression](./give-progression.md)、[give items](./give-items.md)、[give pals](./give-pals.md)、[give pal templates](./give-paltemplate.md) 和 [give Pal eggs](./give-paleggs.md)。


## 响应结构

--8<-- "_snippets/restapi/schemas/give_deprecated.md"

## 错误响应

此端点已废弃，当前构建中可能不存在。如果可用，错误响应体会使用与当前 API 相同的 REST 错误格式。

| HTTP | 错误代码 | 发生条件 |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` 头缺失、格式错误，或与配置的 Bearer 令牌不匹配。 |
| `403` | `MISSING_PERMISSION` | 令牌有效，但不包含此废弃路由的权限。 |
| `400` | `INVALID_JSON` | 提供了请求体，但无法解析为 JSON。 |
| `400` | `REQUEST_FAILED` | 旧版奖励操作在验证或应用请求时失败。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |

## 示例

### Grant EXP and items

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### Grant Pals and eggs

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

## POST `/v1/pdapi/give` — Grant EXP / items / pals / eggs (atomic) { .toc-only }
??? info "POST `/v1/pdapi/give` — Grant EXP / items / pals / eggs (atomic)"
    ## POST `/v1/pdapi/give`
    ### What it does
    Grants rewards to a target player in a single server-side transaction-like operation:

    - EXP and/or
    - items and/or
    - pals and/or
    - eggs
    depending on the request body.

    ### Core behavior
    此端点设计为**原子性**执行：

    - either everything is granted
    - or nothing is granted

    如果任意部分失败（输入无效、背包空间不足、ID 无效等），服务器应拒绝整个请求，而不是只应用其中一部分。

    ### Why this matters
    Admin tooling must not accidentally:

    - give EXP but not items
    - give some items but fail on later items
    - spawn pals without placing items

    Atomic behavior avoids messy states and “support tickets from hell”.

    ### What it can grant
    Depending on your implementation, the request may include:

    - `EXP` — adds experience
    - `Relics` — adds relic points keyed by relic type
    - `TechnologyPoints` — adds tech points
    - `AncientTechnologyPoints` — adds ancient tech points
    - `UnlockTechnology` / `Techs[]` — learn technologies
    - `Items[]` — give one or more items with counts
    - `Pals[]` — give pals by ID + level
    - `PalTemplates[]` — import pal templates by filename
    - `PalEggs[]` — eggs by ID + pal ID / template, optionally with level


    ### 错误响应

    此端点已废弃，当前构建中可能不存在。如果可用，它会使用与当前 API 相同的 REST 错误格式：Bearer 认证失败返回 `INVALID_TOKEN` (`401`)；令牌已认证但无权调用路由时返回 `MISSING_PERMISSION` (`403`)。请求验证失败会以 JSON 错误对象返回；如需端点专用错误码，请迁移到拆分后的奖励端点。

    ### 示例

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### Validation & common failure cases
    管理员遇到错误的常见原因：

    - Inventory space: not enough room for all items → fail the entire request
    - Invalid IDs: unknown `ItemID`, `PalID`, `EggID`, or missing template file → fail
    - Invalid values:
        - negative / zero counts (depending on rules)
        - invalid levels (too low/high, or non-numeric)
        - missing required fields (e.g., no `UserID`)
    - Player not found / not loaded:
        - user ID not known
        - player not currently online (depending on how your server handles offline grants)

    ### 返回
    错误数量和错误消息。如果 `status` 不是 200，请查看 `Errors` 了解发生了多少个错误；`Error` 包含失败项的详细列表。
