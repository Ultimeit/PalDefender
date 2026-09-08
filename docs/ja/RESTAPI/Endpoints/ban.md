# POST /ban/{プレイヤー識別子}



**エンドポイント:** `POST /v1/pdapi/ban/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Punishments.Ban`

## 目的

ユーザーを禁止し、`Banlist.json` に禁止を記録します。現在オンラインの場合、ターゲットはキックされる可能性があります。

## パスパラメータ

- `player_identifier`: `UserId`、`PlayerUID`、または別のサポートされているプレーヤー識別子。

## クエリパラメータ

なし。

## リクエストボディ

オプションの JSON フィールド: `Reason` string および `IP` ブール値。解決された IP アドレスも禁止する場合にのみ、`IP` を `true` に設定します。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/ban.md"

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
| `400` | `IP_UNAVAILABLE` | `IP` は `true` でしたが、サーバーはターゲット ユーザーの IP を解決できませんでした。 |

## 例

### Steam ユーザーを禁止する

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Chargeback fraud"
}
```

### PS5 ユーザーとその解決済み IP の禁止

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Ban evasion",
    "IP": true
}
```

## シナリオ

- モデレーションによる審査後、`UserId` までにプレーヤーを禁止します。
- 将来のスタッフが禁止リストへのエントリを理解できるように、明確な理由を含めます。
- [GET /banlist](banlist.md) を使用して、アクティブなレコードを確認します。禁止関連のデータは `Config.json` で管理されなくなりました。
