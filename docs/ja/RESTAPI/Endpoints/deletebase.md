# POST /deletebase/{base_camp_id}



**エンドポイント:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**認証:** ベアラートークン

**許可:** `REST.Base.Delete`

## 目的

ベースキャンプ ID によってベース/キャンプを削除します。これは破壊的な管理アクションです。

## パスパラメータ

- `base_camp_id`: ベースキャンプ識別子。通常はギルド/ベースデータからコピーされます。

## クエリパラメータ

なし。

## リクエストボディ

オプションの空の JSON object。リクエストを送信する前にIDを確認してください。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | `base_camp_id` パス値は有効な GUID ではありません。 |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` |サーバーは `UPalBaseCampManager` にアクセスできませんでした。 |
| `404` | `BASE_CAMP_NOT_FOUND` |提供された GUID と一致するベースキャンプはありませんでした。 |
| `500` | `DELETE_BASE_FAILED` |ベースキャンプは発見されたが、破壊/清掃は失敗した。 |

## 例

### GUID までにベースキャンプを削除します

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### GUID までに別のベースキャンプを削除します

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## シナリオ

- スタッフによるレビューの後、放棄された基地または壊れた基地を撤去します。
- [GET /guilds](guilds.md) および [GET /guild](guild.md) を使用して、削除する前に正しいキャンプを特定します。
- スタッフ プロセスが所有権とバックアップをすでに検証していない限り、このエンドポイントを定期的なクリーンアップに使用しないでください。
