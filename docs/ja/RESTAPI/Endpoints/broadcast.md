# POST /Broadcast



**エンドポイント:** `POST /v1/pdapi/Broadcast`

**認証:** ベアラートークン

**許可:** `REST.Messages.Broadcast`

## 目的

チャット メッセージをサーバーにブロードキャストします。

## パスパラメータ

なし。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と必須の `Message` string。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/broadcast.md"

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
| `400` | `VALIDATION_FAILED` | `Message` が見つからないか、空であるか、string ではありません。 |

## 例

### 再起動警告をブロードキャストする

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

## シナリオ

- 定期メンテナンスのお知らせ。
- 自動イベント開始メッセージを送信します。
- メッセージが通常のブロードキャスト チャットではなくアラートである必要がある場合は、[POST /Alert](alert.md) を使用します。
