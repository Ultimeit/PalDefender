# :octicons-file-16: `PalSummon.json`

!!! tip "相关 ID 查询"
    召唤文件本身会引用一个 `PalTemplate`。如果需要编辑该模板，请使用 [paldeck.cc/pals](https://paldeck.cc/pals) 查询 `PalID`，[paldeck.cc/passives](https://paldeck.cc/passives) 查询被动词条，[paldeck.cc/skills](https://paldeck.cc/skills) 查询技能 ID。

| 键               | 类型   | 描述                                                                             |
| ----------------- | ------ | --------------------------------------------------------------------------------------- |
| `PalTemplate`     | string | 必填。要使用的 `PalTemplate.json` 文件名（例如 `"OPnubis.json"`）。该文件必须存在于 `Pals/Templates/`。 |
| `Uncapturable`    | bool   | 可选。如果为 `true`，玩家无法捕获该 Pal。省略时默认为 `false`。 |
| `X` / `Y` / `Z`   | float  | 必填。Pal 生成所在的地图坐标。使用 `/getpos` 获取玩家当前位置。 |
| `DisableStatuses` | array  | 可选。要为该 Pal 禁用的状态效果列表。无效或空的状态名会被跳过。可用状态： `DrownCheck`, `Poison`, `Stun`, `Coma`, `Sleep`, `Overwork`, `Drown`, `FallDamage`, `LavaDamage`, `Burn`, `Wetness`, `Freeze`, `Electrical`, `Muddy`, `IvyCling`, `Darkness`, `CollectItem`. |

## 操作说明

1. 先在 `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/` 创建被引用的 Pal 模板。
2. 在 `<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/` 创建召唤文件。
3. 召唤文件名应对应管理员输入的参数，例如 `/summon ArenaBoss` 对应 `ArenaBoss.json`。
4. 在游戏内使用 `/getpos` 获取坐标。使用 RCON 时，请向 `/getpos <UserId>` 传入玩家 ID。
5. 必须保留 `PalTemplate`、`X`、`Y` 和 `Z`。缺少任何坐标都应视为召唤文件无效。
6. 对活动 Boss、Raid Boss 或不应被玩家拥有的装饰性 Pal 使用 `Uncapturable: true`。
7. 除非确实需要禁用大量状态，否则保持 `DisableStatuses` 简短。先只添加对活动重要的状态。
8. 上传前验证 JSON。JSON 不允许注释或末尾多余逗号。
9. 如果你的主机不会立即读取新增文件，请重新加载配置或重启服务器。

## 设置步骤

1. 先创建一个模板，例如 `Pals/Templates/ArenaBoss.json`。
2. 使用 `/givemepal_j ArenaBoss` 测试模板。如果模板在这里失败，请先修复模板，再创建召唤文件。
3. 站在希望 Pal 出现的位置并运行 `/getpos`。复制返回的 `X`、`Y` 和 `Z` 值。
4. 创建 `Pals/Summons/ArenaBossSpawn.json`，并将 `PalTemplate` 设为 `ArenaBoss.json`。
5. 执行 `/summon ArenaBossSpawn`。
6. 如果 Pal 出现得太高、太低或卡在地形中，请先调整 `Z`，再调整 `X` 和 `Y`。

## 示例说明

下面的最小示例会在固定坐标生成 `ArenaBoss.json`，使其无法被捕获，并禁用一小组常见控制/状态效果。这适合活动 Boss。

完整示例展示了可用的 `DisableStatuses` 值。不要默认复制所有状态；只从活动真正需要的状态开始。

## 最小示例

```json
{
    "PalTemplate": "ArenaBoss.json",
    "Uncapturable": true,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": [
        "Poison",
        "Burn",
        "Freeze"
    ]
}
```

## 示例

该文件必须保存到：`<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/ExamplePalSummon.json`
（`ExamplePalSummon` 可以是该文件夹中任意唯一名称。它将作为 `/summon` 的命令参数！）

```json
{
    "PalTemplate": "ExamplePalTemplate.json",
    "Uncapturable": true,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": [
        "DrownCheck",
        "Poison",
        "Stun",
        "Coma",
        "Sleep",
        "Overwork",
        "Drown",
        "FallDamage",
        "LavaDamage",
        "Burn",
        "Wetness",
        "Freeze",
        "Electrical",
        "Muddy",
        "IvyCling",
        "Darkness"
    ]
}
```
