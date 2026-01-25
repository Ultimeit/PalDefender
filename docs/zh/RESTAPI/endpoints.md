# 端点

> **认证：** Bearer token（以下所有端点）

> **基础路径：** `/v1/pdapi`

> **内容类型：** `application/json`（用于 POST 请求）

??? info "GET `/v1/pdapi/version` — PD 版本检查"
    ## GET `/v1/pdapi/version`
    ### 功能
    返回正在运行的 PalDefender 构建/版本信息。

    这是最简单的**健康检查 + 兼容性**端点：

    - 如果此端点响应，则您的 REST API 可访问
    - 您的令牌有效
    - 服务器处于活动状态

    ### 何时使用

    - 检查 REST 设置（URL/端口/令牌）
    - 在工具中检测服务器/插件版本（仪表板、管理面板、脚本）
    - 根据版本保护客户端行为（例如，仅在支持时显示功能）

    ### 返回
    PalDefender 版本对象。

    ### 响应（示例）
    ```json
    {
        "major": 1,
        "minor": 7,
        "patch": 1,
        "build": 3323,
        "version_str": "1.7.1",
        "version_str_long": "1.7.1.3323"
    }
    ```

??? info "GET `/v1/pdapi/guilds` — 列出所有公会"
    ## GET `/v1/pdapi/guilds`
    ### 功能
    返回服务器上所有已知公会的列表/映射，以公会 ID 为键。

    这是一个**目录**端点：它提供标识符 + 基本元数据，您可以使用这些数据查询单个公会。

    ### 何时使用

    - 在管理 UI 中构建公会选择器下拉菜单
    - 发现公会 ID，以便您可以调用 `GET /v1/pdapi/guild/<guild_id>`
    - 跨公会执行审核（例如，列出所有公会名称和所有者）

    !!! note
        将响应视为快照。公会成员资格和元数据在您获取后可能会立即更改。

    ### 返回
    按公会 ID 索引的所有已知公会。

    ### 响应（示例）
    ```json
    {
        "EAF4C152-4B581B5E-4281D299-53459513": {
            "name": "Unnamed Guild",
            "Level": 3,
            "admin": {
                "id": "805C3C33-00000000-00000000-00000000",
                "name": "Zvendson"
            },
            "camp_count": 1,
            "camps": [
                {
                    "id": "584E52BB-40692783-01F26F82-590C53E0",
                    "world_pos": {
                        "x": -321654.0165656156,
                        "y": 214182.5577156711,
                        "z": -762.5510371185613
                    },
                    "map_pos": {
                        "x": 122.40208652651658,
                        "y": -430.86278118870507,
                        "z": -762.5510371185613
                    }
                }
            ],
            "member_count": 1,
            "members": [
                "805C3C33-00000000-00000000-00000000"
            ]
        },
        "E278B61B-4F7366DC-D60E258C-36848A81": {
            "name": "Unnamed Guild",
            "Level": 1,
            "admin": {
                "id": "966E5969-00000000-00000000-00000000",
                "name": "スベンド"
            },
            "camp_count": 0,
            "camps": [],
            "member_count": 1,
            "members": [
                "966E5969-00000000-00000000-00000000"
            ]
        }
    }
    ```

??? info "GET `/v1/pdapi/guild/<guild_id>` — 公会详情"
    ## GET `/v1/pdapi/guild/<guild_id>`
    ### 路径参数

    - `guild_id` (string): 公会标识符，通常从 `GET /v1/pdapi/guilds` 获取
      示例：`EAF4C152-4B581B5E-4281D299-53459513`

    ### 功能
    返回一个公会的完整详情。

    这是**深度视图**：成员、营地/基地以及服务器公开的其他公会特定数据。

    ### 何时使用

    - 在管理工具中显示公会详情页面
    - 检查成员（名称、在线/离线状态）
    - 检查基地/营地和相关公会结构

    ### 返回
    单个公会的详细信息。

    ### 响应（示例）
    ```json
    {
        "name": "Unnamed Guild",
        "Level": 3,
        "admin": {
            "id": "805C3C33-00000000-00000000-00000000",
            "name": "Zvendson"
        },
        "member_count": 1,
        "members": [
            {
                "player_uid": "805C3C33-00000000-00000000-00000000",
                "player_name": "Zvendson",
                "status": "Logout"
            }
        ],
        "camp_count": 1,
        "camps": [
            {
                "id": "584E52BB-40692783-01F26F82-590C53E0",
                "level": 3,
                "world_pos": {
                    "x": -321654.0165656156,
                    "y": 214182.5577156711,
                    "z": -762.5510371185613
                },
                "map_pos": {
                    "x": 122.40208652651658,
                    "y": -430.86278118870507,
                    "z": -762.5510371185613
                },
                "state": "Normal",
                "pals": {
                    "EEB6DA46-4C66DBCE-7304C6B1-CBCACEA1": {
                        "nickname": "OPnubis",
                        "pal_id": "BOSS_Anubis",
                        "npc_id": "None",
                        "skin_id": "None",
                        "gender": "None",
                        "level": 100,
                        "shiny": true,
                        "phisical_health": "Severe",
                        "worker_sick": "DepressionSprain",
                        "san": 0.0,
                        "imported": false,
                        "friendship": 1005,
                        "active_skills": [
                            "DragonBreath",
                            "RockLance",
                            "Unique_Anubis_GroundPunch"
                        ],
                        "learnt_skills": [
                            "DragonBreath"
                        ],
                        "passives": []
                    }
                },
                "buildings": "WIP"
            }
        ],
        "items": {
            "container_id": "F3C7D8A4-496CFBD1-F7884E81-B5B50487",
            "current": 0,
            "max": 54,
            "0": {},
            "1": {},
            "2": {},
            "3": {},
            "4": {},
            "5": {},
            "6": {},
            "7": {},
            "8": {},
            "9": {},
            "10": {},
            "11": {},
            "12": {},
            "13": {},
            "14": {},
            "15": {},
            "16": {},
            "17": {},
            "18": {},
            "19": {},
            "20": {},
            "21": {},
            "22": {},
            "23": {},
            "24": {},
            "25": {},
            "26": {},
            "27": {},
            "28": {},
            "29": {},
            "30": {},
            "31": {},
            "32": {},
            "33": {},
            "34": {},
            "35": {},
            "36": {},
            "37": {},
            "38": {},
            "39": {},
            "40": {},
            "41": {},
            "42": {},
            "43": {},
            "44": {},
            "45": {},
            "46": {},
            "47": {},
            "48": {},
            "49": {},
            "50": {},
            "51": {},
            "52": {},
            "53": {}
        },
        "expeditions": {
            "finished": 0,
            "missions": {
                "DUNGEON_GRASS": false,
                "DUNGEON_FOREST": false,
                "DUNGEON_VOLCANO": false,
                "DUNGEON_DESERT": false,
                "DUNGEON_SNOW": false,
                "DUNGEON_SAKURAJIMA": false,
                "DUNGEON_DARKISLAND": false
            }
        },
        "laboratory": {
            "current_research": "None",
            "researches": {}
        }
    }
    ```

??? info "POST `/v1/pdapi/give` — 授予经验 / 物品 / 帕鲁 / 蛋（原子性）"
    ## POST `/v1/pdapi/give`
    ### 功能
    在单个服务器端类似事务的操作中向目标玩家授予奖励：

    - 经验和/或
    - 物品和/或
    - 帕鲁和/或
    - 蛋
    取决于请求体。

    ### 核心行为
    此端点旨在以**原子性**方式运行：

    - 要么全部授予
    - 要么什么都不授予

    如果任何部分失败（输入无效、背包空间不足、ID 无效等），服务器应拒绝请求并且不要部分应用。

    ### 为什么这很重要
    管理工具不应误导致：

    - 只给经验却未给物品
    - 只给了部分物品，后续物品发放失败
    - 生成帕鲁却未放入物品

    原子行为可避免混乱状态和“地狱般的支持工单”。

    ### 可以授予的内容
    取决于你的实现，请求可能包含：

    - `EXP` — 增加经验
    - `Lifmunks` — 增加 Lifmunk 雕像点数
    - `TechnologyPoints` — 增加科技点
    - `AncientTechnologyPoints` — 增加远古科技点
    - `UnlockTechnology` / `Techs[]` — 解锁科技
    - `Items[]` — 发放一个或多个物品及数量
    - `Pals[]` — 按 ID + 等级发放帕鲁
    - `PalTemplates[]` — 通过文件名导入帕鲁模板
    - `PalEggs[]` — 通过蛋 ID + 帕鲁 ID / 模板生成蛋，可选等级

    ### 验证和常见失败情况
    管理员常见报错原因：

    - 背包空间不足：无法容纳所有物品 → 整个请求失败
    - 无效 ID：未知 `ItemID`、`PalID`、`EggID`，或缺少模板文件 → 失败
    - 无效值：
        - 负数 / 零数量（取决于规则）
        - 无效等级（过低/过高，或非数字）
        - 缺少必填字段（例如没有 `UserID`）
    - 找不到玩家 / 未加载：
        - 用户 ID 未知
        - 玩家当前不在线（取决于服务器如何处理离线发放）

    ### 返回
    错误计数和错误消息。如果状态不是 200，您可以检查 "Errors" 以了解发生了多少错误。在 "Error" 中将有更详细的失败列表。

    ### 请求体（示例）
    ```json
    {
        "UserID": "steam_76561198033245345",
        "EXP": 100000,
        "Lifmunks": 500,
        "TechnologyPoints": 500,
        "AncientTechnologyPoints": 500,
        "UnlockTechnology": "All",
        "Items": [
            { "ItemID": "Launcher_Default_5", "Count": 1 },
            { "ItemID": "ExplosiveBullet", "Count": 500 },
            { "ItemID": "LaserGatlingGun_5", "Count": 1 },
            { "ItemID": "LaserGatlingBullet", "Count": 500 },
            { "ItemID": "MultiGuidedMissileLauncher_5", "Count": 1 },
            { "ItemID": "MissileBullet", "Count": 500 },
            { "ItemID": "EnergyRocketLauncher_5", "Count": 1 },
            { "ItemID": "EnergyLauncherBullet", "Count": 500 }
        ],
        "Pals": [
            { "PalID": "Anubis", "Level": 33 },
            { "PalID": "Kirin", "Level": 13 },
            { "PalID": "AmaterasuWolf", "Level": 19 },
            { "PalID": "WhiteTiger_Ground", "Level": 35 }
        ],
        "PalTemplates": [
            "OPnubis.json"
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Normal_01", "PalID": "Kirin", "Level": 15 },
            { "EggID": "PalEgg_Fire_01", "PalID": "Kirin" },
            { "EggID": "PalEgg_Electricity_01", "PalTemplate": "OPnubis.json", "Level": 15 },
            { "EggID": "PalEgg_Electricity_01", "PalTemplate": "OPnubis.json" }
        ]
    }
    ```

    ### 响应（成功示例）
    状态码：200
    ```json
    {
        "Errors": 0,
        "Error": {}
    }
    ```

    ### 响应（失败示例）
    状态码：400
    ```json
    {
        "Errors": 3,
        "Error": {
            "PalTemplates": [
                "PalTemplate 1: Could not import \"OPnubis.json\". ImportError: File 'D:\\AnotherPalServer\\Pal\\Binaries\\Win64\\PalDefender\\Pals\\Templates\\OPnubis.json' does not exist."
            ],
            "PalEggs": [
                "PalEgg 3: Could not import PalTemplate \"OPnubis.json\". ImportError: File 'D:\\AnotherPalServer\\Pal\\Binaries\\Win64\\PalDefender\\Pals\\Templates\\OPnubis.json' does not exist.",
                "PalEgg 4: Could not import PalTemplate \"OPnubis.json\". ImportError: File 'D:\\AnotherPalServer\\Pal\\Binaries\\Win64\\PalDefender\\Pals\\Templates\\OPnubis.json' does not exist."
            ]
        }
    }
    ```
