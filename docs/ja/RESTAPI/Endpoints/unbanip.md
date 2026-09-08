# POST /unbanip/{ip}



**エンドポイント:** `POST /v1/pdapi/unbanip/<ip>`

**認証:** ベアラートークン

**許可:** `REST.Punishments.UnbanIP`

## 目的

`Banlist.json` の IP アドレスの禁止を解除します。

## パスパラメータ

- `ip`: 禁止を解除する IP アドレス。

## クエリパラメータ

なし。

## リクエストボディ

オプションの JSON フィールド: `Reason` string。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/unbanip.md"

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
| `404` | `BAN_NOT_FOUND` |提供された `ip` は積極的に禁止されていません。 |

## 例

### 理由を付けて IP の禁止を解除する

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Temporary block expired"
}
```

### デフォルトの理由で IP の禁止を解除する

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## シナリオ

- 調査後、IP の禁止を解除します。
- IP レコードがアクティブなままであるため、ユーザーレベルの禁止解除後もプレーヤーがまだブロックされている場合に使用します。
- [GET /banlist](banlist.md) を `ip` とともに使用して結果を確認します。
