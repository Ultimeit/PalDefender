# POST /unban/{user_id}



**エンドポイント:** `POST /v1/pdapi/unban/<user_id>`

**認証:** ベアラートークン

**許可:** `REST.Punishments.Unban`

## 目的

`Banlist.json` のユーザー ID の禁止を解除します。

## パスパラメータ

- `user_id`: 禁止を解除するユーザー ID。

## クエリパラメータ

なし。

## リクエストボディ

オプションの JSON フィールド: `Reason` string。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/unban.md"

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
| `400` | `VALIDATION_FAILED` |オプションのリクエスト フィールドの JSON タイプが間違っています。 |
| `404` | `BAN_NOT_FOUND` |提供された `user_id` は積極的に禁止されていません。 |

## 例

### Steam ユーザーの禁止を解除する

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### デフォルトの理由で PS5 ユーザーの禁止を解除する

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## シナリオ

- 異議申し立ての承認後にユーザーの禁止を解除します。
- 監査証跡の理由を記録します。
- [GET /banlist](banlist.md) を `userId` または `q` とともに使用して結果を確認します。
