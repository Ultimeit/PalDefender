# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>已废弃</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版端点"
    此旧版奖励端点已废弃。建议改用拆分后的奖励端点：[发放进度](./give-progression.md)、[发放物品](./give-items.md)、[发放帕鲁](./give-pals.md)、[发放帕鲁模板](./give-paltemplate.md) 和 [发放帕鲁蛋](./give-paleggs.md)。


## 响应结构

--8<-- "_snippets/zh/restapi/schemas/give_deprecated.md"

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

### 发放经验和物品

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

### 发放帕鲁和蛋

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

??? info "POST `/v1/pdapi/give` — 原子化发放经验 / 物品 / 帕鲁 / 蛋"
    ## POST `/v1/pdapi/give`
    ### 功能
    通过一次类似事务的服务器端操作向目标玩家发放奖励：

    - 经验和/或
    - 物品和/或
    - 帕鲁和/或
    - 蛋，
    具体取决于请求体。

    ### 核心行为
    此端点设计为**原子性**执行：

    - 要么全部发放，
    - 要么全部不发放。

    如果任意部分失败（输入无效、背包空间不足、ID 无效等），服务器应拒绝整个请求，而不是只应用其中一部分。

    ### 为什么这很重要
    管理工具不得意外出现以下情况：

    - 发放经验但未发放物品，
    - 发放部分物品后在后续物品处失败，
    - 生成帕鲁但未放置物品。

    原子行为可避免不一致状态和棘手的支持工单。

    ### 可发放内容
    根据具体实现，请求可能包含：

    - `EXP` — 增加经验值
    - `Relics` — 按遗物类型增加遗物点数
    - `TechnologyPoints` — 增加科技点
    - `AncientTechnologyPoints` — 增加古代科技点
    - `UnlockTechnology` / `Techs[]` — 学习科技
    - `Items[]` — 发放一个或多个物品及其数量
    - `Pals[]` — 按 ID 和等级发放帕鲁
    - `PalTemplates[]` — 按文件名导入帕鲁模板
    - `PalEggs[]` — 按蛋 ID 和帕鲁 ID/模板发放蛋，可选指定等级


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

    ### 验证与常见失败情况
    管理员遇到错误的常见原因：

    - 库存空间：无法容纳全部物品 → 整个请求失败
    - 无效 ID：未知的 `ItemID`、`PalID`、`EggID` 或缺少模板文件 → 请求失败
    - 无效值：
        - 负数或零数量（取决于规则）
        - 无效等级（过低、过高或非数字）
        - 缺少必填字段（例如没有 `UserID`）
    - 找不到或未加载玩家：
        - 用户 ID 未知
        - 玩家当前不在线（取决于服务器处理离线发放的方式）

    ### 返回
    错误数量和错误消息。如果 `status` 不是 200，请查看 `Errors` 了解发生了多少个错误；`Error` 包含失败项的详细列表。
