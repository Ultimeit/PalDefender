# POST /Alert



**エンドポイント:** `POST /v1/pdapi/Alert`

**認証:** ベアラートークン

**許可:** `REST.Messages.Alert`

## 目的

サーバーに警告メッセージを送信します。

## パスパラメータ

なし。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と `Message` string。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/alert.md"

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
| `400` | `BROADCAST_ALERT_FAILED` |サーバーは警告メッセージの送信に失敗しました。 |

## 例

### 再起動アラートを送信する

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Restart now."
}
```

### 複数行のアラートを送信する

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Server restart in 5 minutes.\nPlease return to base."
}
```

## シナリオ

- 優先度の高いサーバー警告を送信します。
- ブロードキャスト後、プレーヤーに緊急の最終通知が必要な場合に使用します。
- アラートはゲーム内で読めるように短くしてください。
