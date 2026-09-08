# POST /banip/{ip}



**エンドポイント:** `POST /v1/pdapi/banip/<ip>`

**認証:** ベアラートークン

**許可:** `REST.Punishments.BanIP`

## 目的

IP アドレスを禁止し、`Banlist.json` に記録します。

## パスパラメータ

- `ip`: IP アドレスを禁止します。

## クエリパラメータ

なし。

## リクエストボディ

オプションの JSON フィールド: `Reason` string および `UserId` string IP 禁止をユーザーに関連付ける必要がある場合。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/banip.md"

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

## 例

### IP のみを禁止する

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Bot traffic"
}
```

### IP を禁止し、GDK ユーザーをアタッチする

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Alt account abuse",
    "UserId": "gdk_2533274898765432"
}
```

## シナリオ

- スタッフによるレビューの後、同じ IP からの繰り返しの虐待を停止します。
- 禁止リストの監査が容易になるように、既知の場合は `UserId` を関連付けます。
- [GET /banlist](banlist.md) を `ip` とともに使用して、アクティブなレコードを確認します。
