# POST /give/progression/{player_identifier}



**エンドポイント:** `POST /v1/pdapi/give/progression/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Progression.Give`

## 目的

プレイヤーに進行値を付与します。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

少なくとも 1 つのサポートされている許可を持つ JSON object: 正の integer `EXP`、正の integer `TechnologyPoints`、正の integer `AncientTechnologyPoints`、またはレリック タイプによってキー設定された空でない object としての `Relics`正のinteger金額。


サポートされているレリック タイプ: `CapturePower`、`HungerReduction`、`SwimSpeed`、`FoodDecayReduction`、`JumpPower`、`GliderSpeed`、`ClimbSpeed`、`StatusAilmentResist`、`StaminaReduction`、`SphereHoming`、`ExpBonus`、 `RainbowPassiveRate`、`MoveSpeed`。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/give-progression.md"

## エラー応答

エラー本体は次の形状を使用します。

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP |エラーコード |それが起こったとき |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` ヘッダーが欠落しているか、形式が不正であるか、構成されたベアラー トークンと一致しません。 |
| `403` | `MISSING_PERMISSION` |トークンは有効ですが、このエンドポイント権限が含まれていません。 |
| `400` | `INVALID_JSON` |リクエスト本文が指定されましたが、JSON として解析できませんでした。 |
| `400` | `REQUEST_FAILED` |ゲーム スレッド コールバックが例外をスローしたか、共有プレーヤー/リソース リゾルバーが失敗しました。 |
| `500` | `REQUEST_TIMEOUT` |内部ゲーム スレッド コールバックは 5 秒以内に完了しませんでした。 |
| `400` | `INVALID_REQUEST` |本体には、`EXP`、`Relics`、`TechnologyPoints`、`AncientTechnologyPoints` のいずれも含まれません。 |
| `400` | `VALIDATION_FAILED` |指定されたプログレッション値が欠落しているか、非 integer、非正、または必要なプログレッション内部が利用できません。 |

## 例

### GDKプレイヤーにEXPを与える

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### PlayerUID によるポイントとレリックの付与

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## シナリオ

- セーブのロールバック後にプレーヤーを補償します。
- 特定のテクノロジーのロックを解除せずにテクノロジーポイントを追加します。
- 特定の [`TechID`](https://paldeck.cc/technology) のロックを解除する場合は、代わりに [POST /learntech](learntech.md) を使用してください。
