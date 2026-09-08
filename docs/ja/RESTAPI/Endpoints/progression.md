# GET /progression/{プレイヤー識別子}



**エンドポイント:** `GET /v1/pdapi/progression/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Progression.Read`

## 目的

EXP、レベル関連の状態、レリックの合計、テクノロジー ポイントの合計などのプレイヤーの進行値を読み取ります。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` |対象のプレイヤー、アカウント、個別キャラクターデータ、記録データ、テクノロジーデータを解決できませんでした。 |
| `500` | `REQUEST_TIMEOUT` |内部ゲーム スレッド コールバックは 5 秒以内に完了しませんでした。 |

## 例

### PS5 ユーザー ID ごとの読み取り進行状況

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### PlayerUID による進行状況の読み取り

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## シナリオ

- 進行を許可する前に、現在の値を確認してください。
- [POST /give/progression](give-progression.md) の後のサポート アクションを確認します。
- 信頼できる管理者ダッシュボードにプレーヤー概要パネルを構築します。
