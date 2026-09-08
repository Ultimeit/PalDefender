# 📄 `Pals/ImportRules/*.json`


Pal インポート ルールは、コマンドまたは API アクションによってインポートされるときに、どの `PalTemplate.json` ファイルを許可、ブロック、または調整するかを制御します。

!!! tip "ID検索"
    `AllowedPalIDs`、`BannedPalIDs`、Pal ごとのルール ファイル名には [paldeck.cc/pals](https://paldeck.cc/pals) を使用します。 `DisallowedPassives` には [paldeck.cc/passives](https://paldeck.cc/passives) を使用します。

## ファイルの場所

|ファイル |目的 |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` |すべての Pal テンプレートのグローバル インポート ルール。 |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` |オプションの Pal ごとのオーバーライド。 Paldeck で [`PalID`](https://paldeck.cc/pals) を検索し、その正確な ID をファイル名として使用します。例: `Anubis.json`。 |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` |参考のために生成されたサンプル ファイル。コピーして名前を変更するまでは、実際の Pal ルールではありません。 |

## キー

|キー |タイプ |説明 |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | `Default.json` のみ。 `AllowAllExceptBanned` では、`BannedPalIDs` を除くすべての Pal が許可されます。 `AllowOnlyListed` では `AllowedPalIDs` のみが許可されます。 |
| `AllowedPalIDs` | array | `Default.json` のみ。 `PalSelectionMode` が `AllowOnlyListed` の場合に許可される [`PalID`](https://paldeck.cc/pals) 値。 |
| `BannedPalIDs` | array | `Default.json` のみ。 [`PalID`](https://paldeck.cc/pals) の値は常に拒否されます。 |
| `MaxValueLimitAction` | string | `BlockImport` は、構成された制限を超えるテンプレートを拒否します。 `ClampToMaxValues` は、設定された制限まで値を下げます。 |
| `DisallowedPassivesAction` | string | `BlockImport` は、リストされたパッシブを含むテンプレートを拒否します。 `RemoveFromPal` は、リストされたパッシブをインポート前に削除します。 |
| `DisallowedPassives` | array | [`PassiveID`](https://paldeck.cc/passives) の値は `DisallowedPassivesAction` の影響を受けます。 |
| `ConditionMode` | string | `None` はルールを通常どおり適用します。 `RequirePalCaptureCount` では、プレーヤーが同じ種の十分な Pals を捕獲した後にのみ、Pal のインポートが許可されます。 |
| `RequiredCaptureCount` |整数 | `ConditionMode` が `RequirePalCaptureCount` (デフォルト `5`) の場合に必要な同種捕獲数。 |
| `Disabled` | bool | `true` の場合、一致するルール セットのインポート チェックを無効にします。 |
| `BanIfPalIsImpossible` | bool | `true`、PalDefender の場合、サーバー設定に従って、不可能な Pal インポートを罰することができます。 |
| `AllowGenderNone` | bool | `false` の場合、`Gender: "None"` を使用するテンプレートはインポート チェックで拒否される可能性があります。 |
| `MaxLevel` |整数 |インポートされたテンプレートに許可される最高の Pal レベル。 |
| `MaxRank` |整数 |インポートされたテンプレートに対して許可される最高のパートナー スキル ランク。 |
| `PalSouls` | object |許容される最大 Pal ソウル値: `Health`、`Attack`、`Defense`、`CraftSpeed`。 |
| `IVs` | object |許可される最大 IV 値: `Health`、`AttackMelee`、`AttackShot`、`Defense`。 |

## 命令セット

1. `Default.json` から始めます。サーバー全体のポリシーに使用します。
2. 1 つの Pal に異なる制限が必要な場合にのみ、Pal ごとのファイルを使用します。
3. Pal ごとのファイルには、Pal ID (例: `Anubis.json`) を使用して名前を付ける必要があります。
4. Pal ごとのファイルに `PalSelectionMode`、`AllowedPalIDs`、または `BannedPalIDs` を置かないでください。これらは `Default.json` に属します。
5. 厳密な管理が必要な場合は、`BlockImport` を使用します。
6. テンプレートを受け入れるが、超過値を減らす場合は、`ClampToMaxValues` を使用します。
7. 失敗したインポートよりも自動クリーンアップを希望する場合は、パッシブに `RemoveFromPal` を使用します。
8. ID を正確に保ち、アップロードする前に JSON を検証します。

## セットアップのウォークスルー

1. `Pals/ImportRules/Default.json` を開くか作成します。
2. グローバル Pal ポリシーを決定します。
   - ほとんどの Pals が許可され、少数のみをブロックしたい場合は、`AllowAllExceptBanned` を使用します。
   - インポートを厳選されたリストに制限する必要がある場合は、`AllowOnlyListed` を使用します。
3. モデレーションのスタイルを決定します。
   - 無効なテンプレートが失敗する厳密なサーバーには `BlockImport` を使用します。
   - テンプレートを受け入れるが、制限を超えるレベル、ランク、ソウル、または IV を減らしたい場合は、`ClampToMaxValues` を使用します。
   - テンプレート全体を拒否するのではなく、不要なパッシブを削除する場合は、パッシブに `RemoveFromPal` を使用します。
4. 許可されていないパッシブを [paldeck.cc/passives](https://paldeck.cc/passives) から追加します。
5. [paldeck.cc/pals](https://paldeck.cc/pals) から禁止または許可された Pals を追加します。
6. 特定の Pal がグローバル ファイルよりも厳しい制限または緩い制限を必要とする場合にのみ、Pal ごとのオーバーライドを追加します。
7. 大きなテンプレートをインポートする前に、まず小さな `PalTemplate.json` でテストします。

## 一般的なセットアップ

### ほとんどの Pals を許可し、いくつかをブロックします

通常の管理者報酬は許可されるが、特定の Pals をインポートすべきでない場合にこれを使用します。

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

### 厳選されたリストのみを許可する

プレーヤーがインポートしたテンプレートを承認済みの Pals に制限する必要がある場合にこれを使用します。

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

この設定では、リストされている 3 つの `PalID` 値のみをインポートできます。超過値は構成された最大値まで減らされ、リストされたパッシブは Pal から削除されます。

## デフォルトの例

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

## Pal ごとのオーバーライドの例

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
