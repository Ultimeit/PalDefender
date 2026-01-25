# 📄 `PalSummon.json`

| 键               | 类型   | 描述                                                                             |
| ----------------- | ------ | --------------------------------------------------------------------------------------- |
| `PalTemplate`     | string | 要使用的 `PalTemplate.json` 的文件名（例如，`"OPnubis.json"`）。                    |
| `Uncapturable`    | bool   | 如果为 `true`，玩家无法捕获该帕鲁。                                       |
| `X` / `Y` / `Z`   | float  | 帕鲁将生成的地图坐标。使用命令 `/getpos` 获取您当前位置。 |
| `DisableStatuses` | array  | 为此帕鲁禁用的状态效果列表。可用状态：`DrownCheck`、`Poison`、`Stun`、`Coma`、`Sleep`、`Overwork`、`Drown`、`FallDamage`、`LavaDamage`、`Burn`、`Wetness`、`Freeze`、`Electrical`、`Muddy`、`IvyCling`、`Darkness`、`CollectItem`。 |

## 示例：

此文件必须存储在：`<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/ExamplePalSummon.json`
（`ExamplePalSummon` 可以是该文件夹中的任何唯一名称。这将是 `/summon` 的命令参数！）

```json
{
    "PalTemplate": "ExamplePalTemplate.json",  // 这是在 `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/` 中的引用文件名
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