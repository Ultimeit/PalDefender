### [<<<](README_ZH_CN.md) 文件类型

#### [English](./PalJSON.md) / 简体中文

# PalJSON

### 目录
- [描述](PalJSON_ZH_CN.md#描述)
- [属性](PalJSON_ZH_CN.md#属性)
- [模板](PalJSON_ZH_CN.md#模板)
- [预设](PalJSON_ZH_CN.md#预设)

## 描述
PalJSON 是一个 JSON 文件，用于定义正在创建的帕鲁的属性。**它必须包含 `CharacterID`，否则创建过程会失败。**

查看默认值：[GitHub/iiLarsH/Chillet/csv's/PalData.csv](https://github.com/iiLarsH/Chillet/blob/698b5ea1190177533dc7924f9af9e40ff8ee4776/csv's/PalData.csv)

## 属性

| 参数 | 值类型 | 值（示例） | 描述 |
|----|--------|------------|------|
| `CharacterID` | 字符串，包含 [PalID](https://pwmodding.wiki/docs/game-data/monster-table) | "..." | 确定该帕鲁是哪个。 |
| `NickName` | 字符串 | "..." |帕鲁的显示名称。 |
| `UniqueNPCID` | 字符串 | "..." |  |
| `Gender` | 整数 | 1 = 男性<br>2 = 女性 |  |
| `Level` | 整数 | 0 - 255 |帕鲁的等级。 |
| `Exp` | 整数 | 0 到 2^63 |帕鲁拥有的经验值。 |
| `IsRarePal` | 布尔值 | true 或 false | 是否为稀有帕鲁。 |
| `MaxHP` | 整数 | 0 到 2^63 |帕鲁的最大血量。 |
| `Hp` | 整数 | 0 到 2^63 |帕鲁当前的血量。 |
| `MaxMP` | 整数 | 0 到 2^63 |帕鲁的最大 MP。 |
| `MP` | 整数 | 0 到 2^63 |帕鲁当前的 MP。 |
| `MaxSP` | 整数 | 0 到 2^63 |帕鲁的最大体力值。 |
| `ShieldMaxHP` | 整数 | 0 到 2^63 |帕鲁的最大盾牌血量。 |
| `ShieldHP` | 整数 | 0 到 2^63 |帕鲁当前的盾牌血量。 |
| `FullStomach` | 浮动数 | 0.0 到 ?? |帕鲁当前的饱腹度。 |
| `MaxFullStomach` | 浮动数 | 0.0 到 ?? |帕鲁的最大饱腹度。最高的默认值在帕鲁中为 `600.0`。 |
| `Support` | 整数 | 0 到 2^31 |  |
| `CraftSpeed` | 整数 | 0 到 2^31 |帕鲁的基础工作速度，默认值为 `100`。 |
| `SanityValue` | 浮动数 | 0.0 到 ?? |帕鲁当前的 SAN（理智值）。 |
| `UnusedStatusPoint` | 整数 | 0 到 2^16 |  |
| `Rank` | 整数 | 0 - 255 |  |
| `RankUpExp` | 整数 | 0 - 255 |  |
| `Rank_HP` | 整数 | 0 - 255 |  |
| `Rank_Attack` | 整数 | 0 - 255 |  |
| `Rank_Defence` | 整数 | 0 - 255 |  |
| `Rank_CraftSpeed` | 整数 | 0 - 255 |  |
| `Talent_HP` | 整数 | 0 - 255 |  |
| `Talent_Melee` | 整数 | 0 - 255 |  |
| `Talent_Shot` | 整数 | 0 - 255 |  |
| `Talent_Defense` | 整数 | 0 - 255 |  |
| `EquipWaza` | 字符串数组，包含 [EPalWazaIDs](../Data%20Lists/EPalWazaIDs_ZH_CN.md) | ["", "", ""] |帕鲁当前装备的技能。 |
| `MasteredWaza` | 字符串数组，包含 [EPalWazaIDs](../Data%20Lists/EPalWazaIDs_ZH_CN.md) | ["", "", "", ""] |帕鲁已学会的技能。 |
| `PassiveSkillList` | 字符串数组，包含 [PassiveSkills](../Data%20Lists/PassiveSkills_ZH_CN.md) | ["", "", "", ""] |帕鲁拥有的所有被动技能。 |

## 模板
文件必须放置在 [`Pal/Binaries/Win64/PalDefender/pals/`](../../README_ZH_CN.md#windows)
```json
{
    "NickName": "",
    "CharacterID": "",
    "UniqueNPCID": "",
    "Gender": 1,
    "Level": 1,
    "Exp": 0,
    "IsRarePal": false,
    "MaxHP": 100,
    "Hp": 100,
    "MaxMP": 100,
    "MP": 100,
    "MaxSP": 100,
    "ShieldMaxHP": 0,
    "ShieldHP": 0,
    "FullStomach": 600.0,
    "MaxFullStomach": 600.0,
    "Support": 100,
    "CraftSpeed": 100,
    "SanityValue": 100.0,
    "UnusedStatusPoint": 0,
    "Rank": 0,
    "RankUpExp": 0,
    "Rank_HP": 0,
    "Rank_Attack": 0,
    "Rank_Defence": 0,
    "Rank_CraftSpeed": 0,
    "Talent_HP": 0,
    "Talent_Melee": 0,
    "Talent_Shot": 0,
    "Talent_Defense": 0,
    "EquipWaza": [],
    "MasteredWaza": [],
    "PassiveSkillList": []
}
```

## 预设
* [OPnubis](PalJSON%20Presets/OPnubis.json) - Anubis，所有属性已最大化。
