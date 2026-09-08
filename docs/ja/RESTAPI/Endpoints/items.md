# GET /items/{プレイヤー識別子}



**エンドポイント:** `GET /v1/pdapi/items/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Items.Read`

## 目的

対象プレイヤーのアイテムを一覧表示します。応答内のアイテム識別子は、[paldeck.cc/items](https://paldeck.cc/items) で検索できます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` |ターゲット プレーヤー、プレーヤーの状態、インベントリ データ、または共通のインベントリ コンテナを解決できませんでした。 |
| `500` | `REQUEST_TIMEOUT` |内部ゲーム スレッド コールバックは 5 秒以内に完了しませんでした。 |

## 例

### Steam プレーヤーのインベントリを読む

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### GDK プレーヤーのインベントリを読み取る

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## シナリオ

- 補償を与える前に在庫を確認してください。
- [POST /give/items](give-items.md) を使用する前に、[`ItemID`](https://paldeck.cc/items) を確認してください。
- 不足しているアイテムに関するレポートのトラブルシューティングを行います。
