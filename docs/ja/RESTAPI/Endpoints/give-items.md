# POST /give/items/{player_identifier}



**エンドポイント:** `POST /v1/pdapi/give/items/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Items.Give`

## 目的

対象のプレイヤーに 1 つ以上のアイテムを与えます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と `Items`、アイテム付与の array。各エントリには [`ItemID`](https://paldeck.cc/items) と正の `Count` が必要です。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` |本体には `Items` array が含まれていません。 |
| `400` | `VALIDATION_FAILED` | 1 つ以上のアイテム付与が無効であるか、サポートされていないか、大きすぎるか、インベントリに収まりません。 |
| `500` | `GRANT_FAILED` |検証は成功しましたが、アイテムをインベントリに追加中にサーバーが失敗しました。 |

## 例

### Steam プレイヤーに弾薬とランチャーを渡す

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### PS5 プレイヤーに通貨を与える

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## シナリオ

- ロールバック後の補償パッケージに使用します。
- 信頼できるサービスが購入アイテムを許可するショップ統合に使用します。
- 最初に [`ItemID`](https://paldeck.cc/items) を検証します。表示名は常に有効な ID であるとは限りません。
