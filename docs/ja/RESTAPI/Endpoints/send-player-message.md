# POST /SendPlayerMessage



**エンドポイント:** `POST /v1/pdapi/SendPlayerMessage`

**認証:** ベアラートークン

**許可:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## 目的

1 人以上のターゲット プレイヤーにメッセージを送信します。

## パスパラメータ

なし。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と `SendType`、`Message`、および `UserID` または `UserIDs` のいずれか。一般的な `SendType` 値には、`PlayerChat`、`PlayerGlobalChat`、`PlayerGuildChat`、`PlayerLogNormal`、`PlayerLogImportant`、および `PlayerLogVeryImportant` が含まれます。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` |リクエストの本文が空です。 |
| `400` | `INVALID_JSON` |リクエスト本文が有効な JSON ではありません。 |
| `400` | `VALIDATION_FAILED` | `SendType`、`Message`、`UserID`、または `UserIDs` が欠落しているか、空であるか、重複しているか、タイプが間違っています。 |
| `400` | `PLAYER_NOT_FOUND` | 1 つ以上のターゲット ユーザー ID またはプレーヤー UID が見つかりませんでした。 |
| `400` | `SEND_MESSAGE_FAILED` |検証は成功しましたが、サーバーはメッセージ送信操作を拒否しました。 |
| `400` | `REQUEST_FAILED` |ゲームスレッドのコールバックが例外をスローしました。 |
| `500` | `REQUEST_TIMEOUT` |内部ゲーム スレッド コールバックは 5 秒以内に完了しませんでした。 |

## 例

### プレーヤー チャットを 1 人のユーザーに送信する

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived."
}
```

### 重要なログを混合ターゲットに送信する

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "The event starts in 10 minutes."
}
```

## シナリオ

- 選択したプレーヤーに直接リスタート警告を送信します。
- 管理パネルからサポートへの返信を送信します。
- 1 つのターゲットには `UserID` を使用し、複数のターゲットには `UserIDs` を使用します (両方ではありません)。
