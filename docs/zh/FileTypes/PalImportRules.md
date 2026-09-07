# 📄 `Pals/ImportRules/*.json`


Pal 导入规则用于控制通过命令或 API 操作导入 `PalTemplate.json` 时，哪些模板允许导入、应被阻止，或需要自动调整。

!!! tip "ID 查询"
    `AllowedPalIDs`、`BannedPalIDs` 和单个 Pal 规则文件名请使用 [paldeck.cc/pals](https://paldeck.cc/pals) 查询。`DisallowedPassives` 请使用 [paldeck.cc/passives](https://paldeck.cc/passives) 查询。

## 文件位置

| 文件 | 用途 |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | 适用于所有 Pal 模板的全局导入规则。 |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | 可选的单个 Pal 覆盖规则。在 Paldeck 上查询 [`PalID`](https://paldeck.cc/pals)，然后使用该精确 ID 作为文件名。例如：`Anubis.json`。 |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | 生成的参考示例文件。复制并重命名之前，它不是实际的 Pal 规则。 |

## 键

| 键 | 类型 | 描述 |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | 仅用于 `Default.json`。`AllowAllExceptBanned` 允许除 `BannedPalIDs` 以外的所有 Pals。`AllowOnlyListed` 只允许 `AllowedPalIDs`。 |
| `AllowedPalIDs` | array | 仅用于 `Default.json`。当 `PalSelectionMode` 为 `AllowOnlyListed` 时允许的 [`PalID`](https://paldeck.cc/pals) 值。 |
| `BannedPalIDs` | array | 仅用于 `Default.json`。始终拒绝的 [`PalID`](https://paldeck.cc/pals) 值。 |
| `MaxValueLimitAction` | string | `BlockImport` 会拒绝超过配置限制的模板。`ClampToMaxValues` 会把数值降低到配置的上限。 |
| `DisallowedPassivesAction` | string | `BlockImport` 会拒绝包含禁用被动的模板。`RemoveFromPal` 会在导入前移除这些被动。 |
| `DisallowedPassives` | array | 受 `DisallowedPassivesAction` 影响的 [`PassiveID`](https://paldeck.cc/passives) 值。 |
| `ConditionMode` | string | `None` 正常应用规则；`RequirePalCaptureCount` 要求玩家先捕获足够数量的同种 Pal 才能导入。 |
| `RequiredCaptureCount` | int | 使用 `RequirePalCaptureCount` 时所需的同种 Pal 捕获数量（默认 `5`）。 |
| `Disabled` | bool | 如果为 `true`，则禁用匹配规则集的导入检查。 |
| `BanIfPalIsImpossible` | bool | 如果为 `true`，PalDefender 可以根据服务器设置处罚不可能合法存在的 Pal 导入。 |
| `AllowGenderNone` | bool | 如果为 `false`，使用 `Gender: "None"` 的模板可能会被导入检查拒绝。 |
| `MaxLevel` | int | 导入模板允许的最高 Pal 等级。 |
| `MaxRank` | int | 导入模板允许的最高伙伴技能等级。 |
| `PalSouls` | object | 允许的 Pal 魂强化上限：`Health`、`Attack`、`Defense`、`CraftSpeed`。 |
| `IVs` | object | 允许的 IV 上限：`Health`、`AttackMelee`、`AttackShot`、`Defense`。 |

## 操作说明

1. 从 `Default.json` 开始。将它用于服务器全局规则。
2. 只有某个 Pal 需要不同限制时，才使用单独的 Pal 文件。
3. 单个 Pal 规则文件必须使用 Pal ID 命名，例如 `Anubis.json`。
4. 不要在单个 Pal 规则文件中设置 `PalSelectionMode`、`AllowedPalIDs` 或 `BannedPalIDs`。这些字段属于 `Default.json`。
5. 如果需要严格审核，请使用 `BlockImport`。
6. 如果想接受模板但降低超限数值，请使用 `ClampToMaxValues`。
7. 如果希望自动清理被动而不是导入失败，请对被动使用 `RemoveFromPal`。
8. ID 必须完全准确。上传前请验证 JSON。

## 设置步骤

1. 打开或创建 `Pals/ImportRules/Default.json`。
2. 决定全局 Pal 策略：
   - 大多数 Pals 允许、只想阻止少数时，使用 `AllowAllExceptBanned`。
   - 导入应限制为精选列表时，使用 `AllowOnlyListed`。
3. 决定审核方式：
   - 对于无效模板应直接失败的严格服务器，使用 `BlockImport`。
   - 想接受模板但降低超限等级、阶级、souls 或 IV 时，使用 `ClampToMaxValues`。
   - 想移除不需要的被动而不是拒绝整个模板时，对被动使用 `RemoveFromPal`。
4. 从 [paldeck.cc/passives](https://paldeck.cc/passives) 添加禁止的被动。
5. 从 [paldeck.cc/pals](https://paldeck.cc/pals) 添加禁止或允许的 Pals。
6. 只有特定 Pal 需要比全局文件更严格或更宽松的限制时，才添加单个 Pal 覆盖规则。
7. 导入大型模板前，先用一个较小的 `PalTemplate.json` 测试。

## 常见设置

### 允许大多数 Pals，只阻止少数

当普通管理员奖励允许，但某些 Pals 不应被导入时使用。

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "BannedPalIDs": [
        "JetDragon",
        "BOSS_Anubis"
    ],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

### 只允许精选列表

当玩家导入的模板应限制为已批准 Pals 时使用。

```json
{
    "PalSelectionMode": "AllowOnlyListed",
    "AllowedPalIDs": [
        "Anubis",
        "Kirin",
        "WeaselDragon"
    ],
    "BannedPalIDs": [],
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 50,
    "MaxRank": 4,
    "PalSouls": {
        "Health": 10,
        "Attack": 10,
        "Defense": 10,
        "CraftSpeed": 10
    },
    "IVs": {
        "Health": 80,
        "AttackMelee": 80,
        "AttackShot": 80,
        "Defense": 80
    }
}
```

在此设置中，只有列出的三个 `PalID` 值可以导入。超过上限的数值会被降低到配置的最大值，列出的被动会从 Pal 身上移除。

## 默认示例

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "BannedPalIDs": [
        "JetDragon"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

## 单个 Pal 覆盖示例

### `Anubis.json`
```json
{
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "AllowGenderNone": false,
    "MaxLevel": 10,
    "MaxRank": 3,
    "PalSouls": {
        "Health": 5,
        "Attack": 5,
        "Defense": 5,
        "CraftSpeed": 5
    },
    "IVs": {
        "Health": 50,
        "AttackMelee": 50,
        "AttackShot": 50,
        "Defense": 50
    }
}
```
