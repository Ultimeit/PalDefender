# GET /guild/{ギルドid}



**エンドポイント:** `GET /v1/pdapi/guild/<guild_id>`

**認証:** ベアラートークン

**許可:** `REST.Guild.Read`

## 目的

詳細なメンバーおよび基地/キャンプ情報を含む 1 つのギルドを返します。

## パスパラメータ

- `guild_id`: ギルド識別子。通常は [GET /guilds](guilds.md) からコピーされます。

## クエリパラメータ

なし。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` |指定された `guild_id` に一致するギルドはありませんでした。 |

## 例

### ギルド名簿とキャンプを読む

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### GUID で別のギルドを読む

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## シナリオ

- ベースを削除する前に、ベースの所有権を調査します。
- サポートリクエストのギルドメンバーとキャンプデータを確認します。
- [POST /deletebase](deletebase.md) を使用して、応答からのキャンプ ID を慎重に使用してください。
