# POST /give/paleggs/{player_identifier}



**エンドポイント:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.PalEggs.Give`

## 目的

ターゲットのプレイヤーに 1 つ以上の Pal の卵を与えます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と `PalEggs`、エッグ付与の array。 `EggID` は [`ItemID`](https://paldeck.cc/items) です。各エッグでは [`PalID`](https://paldeck.cc/pals) または `PalTemplate` の両方を使用することはできません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` |本体には `PalEggs` array が含まれていません。 |
| `400` | `VALIDATION_FAILED` | 1 つ以上の卵子付与が無効であるか、インポートできないか、在庫に収まりません。 |

## 例

### 平らにした卵を Steam プレイヤーに渡します

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### PlayerUID によってテンプレートにバックアップされた卵を与える

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## シナリオ

- Pal をすぐに生成せずにイベントエッグを与えます。
- 単純な卵には `PalID` を使用し、カスタム卵の内容には `PalTemplate` を使用します。
- 卵 [`ItemID`](https://paldeck.cc/items) が無効であるか、プレイヤーのインベントリにスペースがない場合、リクエストは失敗する可能性があります。
