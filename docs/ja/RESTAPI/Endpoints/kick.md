# POST /kick/{プレイヤー識別子}



**エンドポイント:** `POST /v1/pdapi/kick/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Punishments.Kick`

## 目的

禁止記録を作成せずにオンライン プレーヤーをキックします。

## パスパラメータ

- `player_identifier`: `UserId`、`PlayerUID`、または別のサポートされているプレーヤー識別子。

## クエリパラメータ

なし。

## リクエストボディ

オプションの JSON フィールド: `Reason` string。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` |ターゲットのプレイヤーがオンラインにないか、見つかりませんでした。 |

## 例

### 理由を持って GDK プレイヤーをキックする

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "AFK in event area"
}
```

### デフォルトの理由で Steam プレーヤーをキックする

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## シナリオ

- メンテナンス前にプレーヤーを削除します。
- スタックしたプレイヤーをキックして、再接続できるようにします。
- プレーヤーの復帰を許可しない場合は、代わりに [POST /ban](ban.md) を使用してください。
