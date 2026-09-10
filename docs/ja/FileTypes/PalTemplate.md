# 📄 `PalTemplate.json`

<https://paldeck.cc/creator> を使用すると、これらのファイルをより簡単に作成できます。

!!! tip "ID検索"
    `PalID` には [paldeck.cc/pals](https://paldeck.cc/pals)、`Passives` には [paldeck.cc/passives](https://paldeck.cc/passives)、`ActiveSkills` および `LearntSkills` には [paldeck.cc/skills](https://paldeck.cc/skills) を使用します。

|キー |タイプ |説明 |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID` | string |生成する Pal の内部 ID。 Paldeck で有効な [`PalID`](https://paldeck.cc/pals) 値を検索します。 |
| `UniqueNPCID` | string | NPC を生成する Pal の内部 ID。                                               |
| `Nickname` | string | Pal に付けられるオプションのニックネーム。                                                 |
| `SkinId` | string | Pal のスキン オーバーライド (カスタム外観に使用)。 cmd `/getskinids` を使用して ID を取得します。 |
| `Gender` | string | `"Male"`、`"Female"`、または `"None"`。                                                   |
| `Level` |整数 |仲間のレベル。                                                               |
| `Exp` |整数 |経験値ポイント。                                                                  |
| `Shiny` | bool | Pal が光沢があるかどうか。                                                           |
| `PartnerSkillLevel` |整数 | Pal のパートナー スキルのレベル。 1 より小さい値は指定できません。                           |
| `CondensedPals` |整数 |これにマージ/圧縮された Pals の数。                                      |
| `UnusedStatusPoints` |整数 |手動配布に利用可能なステータス ポイント。おそらくプレイヤーのみに使用されますか？    |
| `FriendshipPoints` |整数 | Pal のフレンドシップ値。                                               |
| `PhysicalHealth` | string |身体的な健康状態。有効な名前には、`Healthful`、`MinorInjury`、`Severe`、`Dying`、`DeadBody`、`CloudCemetery` があります。 |
| `WorkerSick` | string |労働者の病気の状態。有効な名前には、`None`、`Cold`、`Sprain`、`Bulimia`、`GastricUlcer`、`Fracture`、`Weakness`、`DepressionSprain`、`DisturbingElement` があります。 |
| `ImportedCharacter` | bool | Pal をインポートされた文字としてマークします。                                    |
| `HP` / `SP` / `MP` |番号 |基本的なヘルス、スタミナ、マナの値。`HP` は、このテンプレートを参照する PalSummon および REST 召喚を含め、生成された Pal の最大 HP として使用されます。 |
| `Shield` |番号 |シールド値。                                                              |
| `Hunger` / `MaxHunger` |整数 |現在の空腹値と最大空腹値。                                                      |
| `SAN` |整数 |正気度 (Pal の精神的安定)。                                               |
| `Support` |整数 |サポート レベル (AI の動作とスキルに使用)。                                    |
| `CraftSpeed` |整数 |製作速度の乗数。                                                          |
| `PalSouls` | object |パッシブソウルボーナス。含まれるもの: `Health`、`Attack`、`Defense`、`CraftSpeed`。推奨される正常値は、インポート ルールによって制御されます。 |
| `IVs` | object |個人のステータス値。含まれるもの: `Health`、`AttackMelee`、`AttackShot`、`Defense`。推奨される正常値は、インポート ルールによって制御されます。 |
| `ActiveSkills` | array |装備スキル一覧。 PalDefender 1.9.0 では、管理用 PalTemplate が 3 つのエントリに切り詰められません。すべてのエントリーは装備されたままになります。 Paldeckで有効な[スキルID](https://paldeck.cc/skills)を検索します。通常のゲーム/UI の動作では、標準のスロット数が想定される場合があります。 |
| `LearntSkills` | array | Pal が学習し、交換できるスキル。ここにアクティブスキルを置くことは避けてください。 Paldeckで有効な[スキルID](https://paldeck.cc/skills)を検索します。 |
| `Passives` | array | Pal が持つ受動的特性。通常の Pals は最大 4 つのパッシブを使用する必要があります。 Paldeck で有効な [`PassiveID`](https://paldeck.cc/passives) 値を検索します。 |
| `ExtraWorkSuitabilities` | object |作業の種類とレベルを強化しました (例: `"Mining": 2`)。利用可能な作業タイプ: `EmitFlame`、`Watering`、`Seeding`、`GenerateElectricity`、`Handcraft`、`Collection`、`Deforest`、`Mining`、`OilExtraction`、`ProductMedicine`、 `Cool`、`Transport`、`MonsterFarm`。  |
| `DisableWorkPreferences` | array | Pal が実行を拒否する作業タイプ。利用可能な作業タイプ: `BaseCampBattle`、`EmitFlame`、`Watering`、`Seeding`、`GenerateElectricity`、`Handcraft`、`Collection`、`Deforest`、`Mining`、`OilExtraction`、 `ProductMedicine`、`Cool`、`Transport`、`MonsterFarm`。 |

## 命令セット

1. `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/` のカスタム Pal ごとに 1 つの JSON ファイルを作成します。
2. `RaidRewardAnubis.json` などの一意のファイル名を使用します。コマンドでは通常、`RaidRewardAnubis` または `RaidRewardAnubis.json` を使用できます。
3. `PalID` を必ず含めてください。それ以外はすべてオプションですが、値が欠落している場合は、デフォルトの PalDefender または Palworld が使用されます。
4. `Level` を `1` 以上、`PartnerSkillLevel` を `1` 以上に保ちます。
5. 装備されている攻撃を `ActiveSkills` に、その他の既知の攻撃を `LearntSkills` に入力します。 PalDefender は、追加のアクティブなエントリを学習済みスキルに移動しなくなりました。
6. Pals、スキル、パッシブ、スキン、ワークタイプには正確な ID を使用します。間違った ID はインポートに失敗するか、無視される場合があります。
7. アップロードする前に JSON を検証します。 JSON では、コメントや末尾のカンマは許可されません。
8. テンプレートがインポートされても値が変更またはブロックされている場合は、サーバーの `Pals/ImportRules/Default.json` および Pal ごとのオーバーライド ファイルを確認してください。

## セットアップのウォークスルー

1. テンプレートの用途を決定します。単純な管理者報酬、イベント ボス、テスト用 Pal、または召喚用のスポーン テンプレートです。
2. [paldeck.cc/pals](https://paldeck.cc/pals) で `PalID` を選択します。表示名は必ずしもファイル ID であるとは限らないため、ID を正確にコピーしてください。
3. 制御するフィールドのみを追加します。短いテンプレートは、非常に大きなテンプレートよりもデバッグが簡単です。
4. [paldeck.cc/skills](https://paldeck.cc/skills) からスキルを選択します。装備した攻撃を `ActiveSkills` に入力します。他の既知の攻撃を `LearntSkills` に追加します。
5. [paldeck.cc/passives](https://paldeck.cc/passives) からパッシブを選択します。通常の使用では、サーバーが意図的にそれ以上のパッシブを許可しない限り、最大 4 つのパッシブを保持します。
6. ファイルを `Pal/Binaries/Win64/PalDefender/Pals/Templates/` に保存します。
7. 最初に `/givemepal_j <filename>` を使用してテストします。その後、`/givepal_j`、`/spawnpal_j`、`/giveegg_j`、REST、API、または `PalSummon.json` に同じテンプレートを使用します。

## 例の説明

以下の最小限の例では、3 つの装備された攻撃と 2 つのパッシブを備えたレベル 50 のアヌビスを作成します。必須の `PalID` といくつかの共通フィールドのみが含まれるため、テストに適しています。

より大きな例は意図的に極端になっています。魂、個体値、スキル、パッシブ、および作業適合性オーバーライドで利用可能な構造を示します。インポート ルールを使用するサーバーでは、高い値がクランプまたはブロックされる場合があります。

## 最小限の例

```json
{
    "PalID": "Anubis",
    "Nickname": "Arena Anubis",
    "Gender": "None",
    "Level": 50,
    "PartnerSkillLevel": 1,
    "HP": 3500,
    "SAN": 100,
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "RockLance"
    ],
    "Passives": [
        "Legend",
        "CraftSpeed_up3"
    ]
}
```

## 例

このファイルは `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json` に保存する必要があります。
(`ExamplePalTemplate` は、そのフォルダー内で任意の一意の名前にすることができます。これは、`/givepal_j` および `/spawnpal_j` のコマンド引数になります。)

```json
{
    "PalID": "Anubis",
    "Nickname": "OPnubis",
    "Gender": "None",
    "Level": 255,
    "Shiny": true,
    "PartnerSkillLevel": 255,
    "HP": 999999,
    "SP": 999999,
    "MP": 999999,
    "Hunger": 999999,
    "MaxHunger": 999999,
    "SAN": 999999,
    "Support": 999999,
    "CraftSpeed": 999999,
    "PalSouls": {
        "Health": 255,
        "Attack": 255,
        "Defense": 255,
        "CraftSpeed": 255
    },
    "IVs": {
        "Health": 255,
        "AttackMelee": 255,
        "AttackShot": 255,
        "Defense": 255
    },
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "Unique_Anubis_LowRoundKick"
    ],
    "Passives": [
        "Legend",
        "PAL_ALLAttack_up3",
        "Deffence_up3",
        "Vampire",
        "Stamina_Up_3",
        "EternalFlame",
        "PAL_Sanity_Down_3",
        "Invader",
        "SwimSpeed_up_3",
        "Rare",
        "Nushi",
        "PAL_FullStomach_Down_3",
        "CraftSpeed_up3",
        "Salvation",
        "Witch",
        "MoveSpeed_up_3",
        "SwimSpeed_up_2",
        "CraftSpeed_up2",
        "Deffence_up2",
        "ElementBoost_Normal_2_PAL",
        "PAL_FullStomach_Down_2",
        "ElementBoost_Dragon_2_PAL",
        "ElementBoost_Earth_2_PAL",
        "PAL_ALLAttack_up2",
        "ElementBoost_Fire_2_PAL",
        "ElementBoost_Ice_2_PAL",
        "Stamina_Up_1",
        "TrainerLogging_up1",
        "ElementBoost_Thunder_2_PAL",
        "ElementBoost_Aqua_2_PAL",
        "ElementBoost_Dark_2_PAL",
        "TrainerMining_up1",
        "TrainerWorkSpeed_UP_1",
        "SalePrice_Up_1",
        "Test_PalEgg_HatchingSpeed_Up",
        "MoveSpeed_up_2",
        "CoolTimeReduction_Up_1",
        "ElementBoost_Leaf_2_PAL",
        "TrainerDEF_UP_1",
        "TrainerATK_UP_1",
        "PAL_Sanity_Down_2",
        "ElementResist_Normal_1_PAL",
        "ElementBoost_Dragon_1_PAL",
        "ElementResist_Leaf_1_PAL",
        "PAL_ALLAttack_up1",
        "ElementBoost_Thunder_1_PAL",
        "ElementResist_Dark_1_PAL",
        "ElementBoost_Ice_1_PAL",
        "PAL_FullStomach_Down_1",
        "ElementResist_Dragon_1_PAL",
        "ElementResist_Earth_1_PAL",
        "SalePrice_Up_2",
        "Stamina_Up_2",
        "ElementBoost_Leaf_1_PAL",
        "Deffence_up1",
        "ElementResist_Ice_1_PAL",
        "ElementBoost_Aqua_1_PAL",
        "CoolTimeReduction_Up_2",
        "ElementResist_Thunder_1_PAL",
        "MoveSpeed_up_1",
        "Alien",
        "PAL_Sanity_Down_1",
        "ElementBoost_Earth_1_PAL",
        "ElementBoost_Fire_1_PAL",
        "CraftSpeed_up1",
        "SwimSpeed_up_1",
        "ElementResist_Fire_1_PAL",
        "ElementBoost_Dark_1_PAL",
        "ElementResist_Aqua_1_PAL",
        "ElementBoost_Normal_1_PAL"
    ],
    "ExtraWorkSuitabilities": {
        "EmitFlame": 5,
        "Watering": 5,
        "Seeding": 5,
        "GenerateElectricity": 5,
        "Handcraft": 5,
        "Collection": 5,
        "Deforest": 5,
        "Mining": 5,
        "OilExtraction": 5,
        "ProductMedicine": 5,
        "Cool": 5,
        "Transport": 5,
        "MonsterFarm": 5,
        "Anyone": 5
    }
}
```
