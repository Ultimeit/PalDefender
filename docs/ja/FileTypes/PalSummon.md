# 📄 `PalSummon.json`

PalSummon ファイルは、`/summon <filename>` で起動される固定場所での遭遇を定義します。ファイルを `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/` に保存し、参照された PalTemplate を `Pals/Templates/` に保存します。

!!! tip "ID検索"
    `PalID` には [paldeck.cc/pals](https://paldeck.cc/pals)、パッシブには [paldeck.cc/passives](https://paldeck.cc/passives)、参照テンプレートで使用されるスキル ID には [paldeck.cc/skills](https://paldeck.cc/skills) を使用します。

## エンカウンターキー

|キー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `PalTemplate` | string |必須 | `Pals/Templates/` のテンプレートのファイル名。 `.json` は省略できます。 |
| `BossBattleName` | string | Pal ID |アナウンス、ログ、Webhook、および被害結果で使用される表示名。 |
| `Uncapturable` | bool | `false` |召喚された Pal が捕らえられないようにする。 |
| `CapturableAtHealthPercent` |番号 | `15` |捕獲可能な場合は、この HP パーセンテージ以下でのみ捕獲を有効にします (`0`–`100`)。 `Uncapturable` が `true` の場合は無視されます。 |
| `DisableAI` | bool | `false` |通常のAIを無効化します。回避などの一部の受動的な動作が依然として発生する可能性があります。 |
| `DisableDamageMeter` | bool | `false` |追跡、結果ダイアログ、ランク報酬を無効にします。代わりに、`Default` 報酬がすべてのオンライン プレーヤーに付与されます。 |
| `SpawnScale` |番号 | `1.0` |視覚的/物理的なサイズの乗数。正でない値は `1.0` に戻ります。 |
| `HealthMultiplier` |番号 | `1.0` |最大体力乗数。は有限でゼロより大きくなければなりません。 |
| `DamageTakenMultiplier` |番号 | `1.0` |受けたダメージの乗数。負の値は `1.0` に戻ります。 |
| `DamageDealtMultiplier` |番号 | `1.0` |与えられたダメージの乗数。負の値は `1.0` に戻ります。 |
| `X`、`Y`、`Z` |番号 |必須 |地図座標。 `/getpos` を使用して取得します。 |
| `DisableStatuses` | array |空 |抑制するステータス名。無効な名前はスキップされます。 |
| `Rewards` | object または array |空 |ランク別およびデフォルトの[報酬定義](#damage-meter-and-rewards)（任意）。object 形式を推奨します。 |

`CapturableAt`、`CapturableAtPercent`、および `capturable_at` は、互換性エイリアスとして受け入れられます。 `HPMultiplier`、`AdditionalEnemyMaxHPRate`、`AdditionalEnemyReceiveDamageRate`、および `AdditionalEnemyInflictDamageRate` も使用できますが、表内の名前が優先されます。

## ダメージメーターと報酬 { #damage-meter-and-rewards }

召喚されたパルが死亡または捕獲されると、報酬が確定します。ダメージランキングは与えたダメージが多い順に並びます。結果ダイアログには上位 5 名が表示され、上位 3 名が強調されます。受信するプレイヤーが上位 5 名以外の場合は、そのプレイヤー自身の順位も表示されます。

ダメージ追跡が有効になっている場合、各参加プレイヤーは次のように処理されます。

1. PalDefender は、プレイヤーの最終ランクに一致する数値 `Rewards` キーを探します。
2. その正確なランクが存在しない場合、PalDefender は `Rewards.Default` を使用します。
3. どちらも存在しない場合、そのプレイヤーは報酬を受け取りません。
4. 選択した報酬は、そのプレイヤーに対して個別にロールされます。したがって、同じ `Default` 定義を使用する 2 人のプレーヤーは、異なるランダムな結果を受け取る可能性があります。

ランク報酬を受け取れるのは、エンカウント終了時にもオンラインで、有効なプレイヤーコントローラーを持つ参加者だけです。番号付き報酬は `Default` と加算されるのではなく、その順位の `Default` を置き換えます。

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

この例では、1 位は両方の保証ドロップを受け取り、2 位はランダムな量の EXP を受け取り、その他のランク付けされた参加者はそれぞれ、75% の確率で 1,000 Money を受け取ります。

ランク キーは、`"1"`、`"2"`、`"10"` など、JSON オブジェクト キーとして記述された正の整数である必要があります。 `"0"`、負のランク、および任意の名前は無効です。 `Default` は大文字と小文字を区別せずに照合されます。

??? note "配列形式"
    `Rewards` は配列である場合もあります。配列要素 0 はランク 1、要素 1 はランク 2 などとなります。配列形式では `Default` を定義できないため、オブジェクト形式の方が明確であり、推奨されます。

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### 報酬定義の構造

すべてのランクと `Default` には 1 つの報酬定義が含まれます。定義には次の両方を含めることができます。

- `Drops`: エントリは直接かつ独立して評価されます。
- `Pools`: エントリの選択方法を制御するグループ。

また、進行短縮表現 `EXP`、`TechnologyPoints`、および `AncientTechnologyPoints` が含まれる場合もあります。短縮表記は保証されており、独自の `Chance`、`Weight`、または `Unique` 設定が必要ない場合に便利です。

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### 報酬エントリーの種類

各エントリは、報酬タイプを 1 つだけ定義する必要があります。同じエントリ内でアイテム、卵、進行フィールドを組み合わせないでください。

|報酬 |必須フィールド |オプションのフィールド |メモ |
| --- | --- | --- | --- |
|アイテム | `ItemID` | `Count`、`Chance`、`Weight`、`Unique` | `Count` のデフォルトは `1` です。 |
|パルエッグ | `EggID`、`PalTemplate` | `Count`、`Level`、`Chance`、`Weight`、`Unique` | `Count` のデフォルトは `1` です。 `Level: 0` はテンプレートのレベルを使用します。 |
|経験 | `EXP` | `Chance`、`Weight`、`Unique` | `EXP` 値は量または範囲です。 |
|技術のポイント | `TechnologyPoints` | `Chance`、`Weight`、`Unique` |フィールド値は量または範囲です。 |
|古代技術のポイント | `AncientTechnologyPoints` | `Chance`、`Weight`、`Unique` |フィールド値は量または範囲です。 |

`Chance`、`Weight`、および `Unique` は、以下で説明するコンテキストでのみ有効です。パーサーによってフィールドが受け入れられたとしても、それがすべての分散モードに影響を与えるわけではありません。

上記の正規のフィールド名が推奨されます。パーサーは次のエイリアスも受け入れます。

|正規フィールド |受け入れられるエイリアス |
| --- | --- |
| `ItemID` | `ItemId`、`ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`、`Num` |
| `EXP` | `Exp`、`Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### 固定値、範囲、確率

金額には、固定の整数または包括的な範囲を指定できます。

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- `Count`、EXP、およびテクノロジー ポイントの量は、少なくとも `1` の整数である必要があります。
- 範囲には `Min` と `Max` の両方が必要であり、`Max` は `Min` 未満であってはなりません。
- `"1-3"` などのテキスト範囲は無効です。 `{ "Min": 1, "Max": 3 }` を使用してください。
- 卵 `Level` は `0` になる可能性があります。これにより、参照された PalTemplate からのレベルが維持されます。正のレベルはテンプレート レベルをオーバーライドし、卵が付与されるときはレベル 255 に上限が設定されます。
- `Chance` は、オプションの `%` を含む数値または数値テキスト (`30`、`30.5`、または `"30%"`) を受け入れます。
- `Chance: 0` は決して成功せず、`Chance: 100` は常に成功し、値は `0` と `100` の間にある必要があります。
- チャンスが厳密に 0 ～ 100 の場合、生成されるロールは設定された値よりも低くなければなりません。したがって、正確に `30.0` のロールは、`30` の `Chance` には失敗します。

### 直接ドロップ

`Drops` のすべてのエントリは独立して評価されます。隣接するエントリ間には、1 つを選択する関係はありません。 `Chance` が欠落している場合は、`100` を意味します。

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

Money は保証されています。弾薬、EXP、テクノロジー ポイントはそれぞれ独自のチャンス ロールを行います。 0、1、2、または 3 つのオプションのドロップすべてが成功する可能性があります。

`Weight` および `Unique` は、直接の `Drops` では機能せず、警告が生成されます。オプションの直接ドロップには `Chance` を使用します。

## 戦利品プール

プールは最初に独自の `Chance` をロールします。プールに障害が発生した場合、そのエントリはどれも考慮されません。成功すると、`Mode` によってエントリの評価方法が決定されます。

|プールキー |タイプ |デフォルト |説明 |
| --- | --- | --- | --- |
| `Name` |文字列 |空 |オプションの診断ラベル。選択には影響しません。 |
| `Mode` |文字列 | `OneOf` | `OneOf`、`Pick`、`All`、または `Independent`。照合では大文字と小文字が区別されません。 |
| `Chance` |数値またはパーセンテージのテキスト | `100` |プール全体がアクティブになる可能性があります。 |
| `Rolls` |整数 | `1` | `Pick` 内の選択の数。他のモードでは無視されます。 |
| `Unique` |ブール | `true` | `Pick` のデフォルトの繰り返しポリシー。エントリによってオーバーライドされる場合があります。 |
| `Entries` |配列 |必須 |報酬エントリの空でないリスト。 |

`One` は `OneOf` のエイリアスとして、`PickN` は `Pick` のエイリアスとして受け入れられますが、正規のモード名が推奨されます。

|モード |エントリーは何件まで許可されますか? | `Weight` を使用しますか? |エントリ `Chance` を使用しますか? | `Rolls` / `Unique` を使用しますか? |
| --- | --- | --- | --- | --- |
| `OneOf` |プールが成功した場合は 1 つだけ |はい |いいえ |いいえ |
| `Pick` |最大 `Rolls` の選択 |はい |いいえ |はい |
| `All` |プールが成功した場合は、すべてのエントリが 1 回 |いいえ |いいえ |いいえ |
| `Independent` |ゼロからすべてのエントリ |いいえ |はい |いいえ |

All の 4 つのモードは引き続きプールレベルの `Chance` を使用します。 1 つの報酬定義内の複数のプールは個別に処理され、その結果は直接 `Drops` に追加されます。

### `OneOf`: 1 つの重み付けされた結果

`OneOf` がデフォルトのモードです。プールレベルのチャンスが成功した場合、ちょうど 1 つのエントリが選択されます。エントリの確率は、その `Weight` をすべてのエントリの重みの合計で割ったものです。

```json
{
    "Pools": [
        {
            "Name": "Equipment jackpot",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

重みは合計 20 です。プールが成功することを条件として、4 つのエントリの確率は 35%、35%、25%、および 5% になります。プール自体は 35% の確率でのみアクティブになるため、卵の絶対確率は `35% × 5% = 1.75%` です。

- `Weight` が欠落している場合、デフォルトは `1` になります。
- `Weight` は少なくとも `1` の整数でなければなりません。重み `0` を割り当てる代わりにエントリを削除します。
- `OneOf` は常に 1 回選択するため、`Rolls` は無視され、警告が生成されます。
- エントリレベルの `Chance` は無視され、警告が生成されます。 `Weight` を使用して、相対的な選択確率を制御します。
- `Unique` は、エントリが 1 つだけ選択されているため、実質的な効果はありません。

### `Pick`: 繰り返しのない複数の重み付けされた結果

`Pick` は重み付き選択を `Rolls` 回繰り返します。デフォルトの `Unique: true` では、選択したエントリは次の選択の前に削除され、再度選択することはできません。重みは、各選択後に残りのエントリから再計算されます。

```json
{
    "Pools": [
        {
            "Name": "Choose two different rewards",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

これにより、2 つの異なるエントリが許可されます。 `Rolls` が使用可能な一意のエントリの数より大きい場合、エントリがなくなると選択が停止します。それはエラーではありません。

### `Pick`: 繰り返しの結果を許可します

選択したエントリを後のロールで使用できるようにするには、プールの `Unique` を `false` に設定します。同じアイテムの繰り返しの付与は、配信前にマージされます。

```json
{
    "Pools": [
        {
            "Name": "Three supply rolls",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

All 3 つのロールで Money が選択される場合もあれば、すべてが弾薬を選択する場合もあり、結果が混在する場合もあります。たとえば、Money を 2 回選択すると、2 つの個別の許可ではなく、10,000 の Money 許可が 1 つ生成されます。

### `Pick`: エントリごとに `Unique` をオーバーライドします

エントリレベルの `Unique` は、そのエントリのプールのデフォルトのみをオーバーライドします。これにより、同じプール内で繰り返し可能な共通報酬と 1 回限りのジャックポット報酬が可能になります。

```json
{
    "Pools": [
        {
            "Name": "Repeatable currency with unique jackpots",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

Money は、エントリに `Unique: false` と表示されているため、選択後も候補リストに残ります。鎧とヘルメットはプールから `Unique: true` を継承し、選択後に削除されます。逆も有効です。プールでは `Unique: false` を使用できますが、特定のエントリでは `Unique: true` が使用されます。

### `All`: すべてのエントリを許可します

`All` は、プールレベルの `Chance` が成功したときに、すべてのエントリを 1 回だけ許可します。

```json
{
    "Pools": [
        {
            "Name": "Complete reward bundle",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`Weight`、エントリーレベルの `Chance`、および `Unique` は、`All` には影響しません。 `Rolls` は無視され、警告が生成されます。バンドル全体をオプションにするには、プールの `Chance` を設定します。個々のエントリをオプションにするには、代わりに `Independent` を使用するか、直接 `Drops` を使用します。

### `Independent`: すべてのエントリを個別にロールします

`Independent` はすべてのエントリをチェックし、各エントリ独自の `Chance` を使用します。エントリをまったく許可しないことも、1 つのエントリを許可することも、複数のエントリを許可することも、すべてのエントリを許可することもできます。

```json
{
    "Pools": [
        {
            "Name": "Independent bonus rolls",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

まず、プールは 80% の確率でアクティブになります。アクティブ化すると、そのエントリで `Chance` が省略されるため、Money が保証されます。他の 3 つのエントリは、独立して 50%、10%、および 5% をロールします。

- 欠落しているエントリ `Chance` のデフォルトは `100` です。
- `Weight` および `Unique` はこのモードに影響しません。
- すべてのエントリが 1 回チェックされるため、`Rolls` は無視され、警告が生成されます。

### 直接ドロップと複数のプールの組み合わせ

1 人の受信者が複数の独立して構造化された報酬レイヤーを受け取る必要がある場合は、複数のプールを使用します。

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "One equipment item",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "Two supply rolls",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "Rare independent bonuses",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

直接の Money および EXP は常に適用されます。最初のプールは 1 つの装備アイテムを追加し、2 番目のプールは交換を伴う 2 つの加重サプライ選択を行い、3 番目のプールは 2 つの独立したボーナス ロールを行います。プールは互いに競合しないため、プレーヤーはすべてのプールから結果を受け取ることができます。

### パルエッグの報酬

卵には `EggID` と `PalTemplate` の両方が必要です。テンプレートは `Pals/Templates/` からロードされ、`.json` は省略できます。 `Count` は、付与される卵の数を制御します。 `Level: 0` または省略されたレベルはテンプレート レベルを維持します。正の固定値または範囲はそれをオーバーライドします。

```json
{
    "Pools": [
        {
            "Name": "One random egg reward",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

報酬が付与されたときにエッグテンプレートをインポートできない場合、PalDefender はエラーをログに記録し、そのエッグ報酬をスキップします。

### 繰り返された結果をマージする

直接ドロップとすべてのプールの結果は、配信前に結合されます。

- 同じ `ItemID` を持つアイテムは、その数を加算することによってマージされます。
- エッグは、`EggID`、`PalTemplate`、およびロールされた `Level` がすべて同一である場合にのみマージされます。
- EXP、技術ポイント、古代技術ポイントが合算されます。
- 付与可能なアイテムとテクノロジー ポイントの合計は、符号付き 32 ビットの最大値 (`2,147,483,647`) に制限されます。

これは、`Pick` の結果が繰り返されても、報酬リクエストに重複した在庫行が作成されないことを意味します。ロールレベルが異なる卵は別個の報酬のままです。

### `DisableDamageMeter` 配布

`DisableDamageMeter` が `true` の場合、PalDefender はダメージ リーダーボードを構築せず、数値ランク報酬を使用しません。代わりに、呼び出されたパルにダメージを与えなかったプレイヤーも含め、*エンカウント終了時にオンラインになっているすべてのプレイヤー**に対して個別に `Rewards.Default` をロールします。

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

Money はすべてのオンライン プレーヤーに付与されます。各プレイヤーは、2 つのオプションのポイント報酬を個別にロールします。 `Default` が欠落しているか空の場合、このモードでは誰も報酬を受け取りません。PalDefender はログに警告を書き込みます。

### 無効で無視された組み合わせ

無効な報酬データにより、PalSummon ファイルをロードできません。不明なフィールドや文脈上無視されるフィールドでは警告が生成されるため、スペルミスや無効な設定が PalDefender ログに表示されます。

|構成 |結果 |
| --- | --- |
| 1 つのエントリには `ItemID` と `EXP` の両方が含まれています。エラー: エントリで定義できる報酬タイプは 1 つだけです。 |
|報酬エントリにはアイテム、卵、または進行フィールドがありません。エラー: PalDefender は何を付与すればよいのかわかりません。 |
| `Count: 0`、`Weight: 0`、または `Rolls: 0` |エラー: これらの値は少なくとも `1` である必要があります。 |
|範囲に `Min` または `Max` が省略されているか、`Max < Min` が含まれています。エラー。 |
| `Chance` は `0`–`100` の外にあります |エラー。 |
|プールに `Entries`、空の `Entries` 配列、または配列以外の値がありません。エラー。 |
| `Chance` は、`OneOf`、`Pick`、または `All` エントリに配置されます。警告;エントリーチャンスは無視されます。 |
| `Rolls` は `OneOf`、`All`、または `Independent` に設定されています。警告; `Rolls` は無視されます。 |
| `Weight` または `Unique` は直接 `Drops` に配置されます。警告;直接ドロップするには `Chance` を使用してください。 |
| `Wieght` などの不明なフィールドが存在します。警告;フィールドは未使用です。 |

コメントや末尾のカンマのない有効な JSON を使用してください。召喚がまだロードされている場合でも、ロード警告を確認してください。警告は通常、効果のない設定を示します。

## 完全な例

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Arena Anubis",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "HealthMultiplier": 8.0,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "Winner bonus",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## 検証チェックリスト

1. まず、`/givemepal_j <template>` を使用して、参照されたテンプレートをテストします。
2. `X`、`Y`、および `Z` には `/getpos` を使用します。 RCON は、`/getpos` に UserId を提供する必要があります。
3. コメントや末尾のカンマのない有効な JSON を使用します。
4. 1 つの報酬エントリには、報酬タイプを 1 つだけ指定します。
5. 各プールに空でない `Entries` array があり、選択した `Mode` で有効なフィールドだけを使用していることを確認します。
6. `/summon <filename>` を実行し、PalDefender ログで詳細な検証エラーと警告を確認します。
