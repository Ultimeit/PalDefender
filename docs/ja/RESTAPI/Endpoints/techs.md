# GET /techs/{プレイヤー識別子}



**エンドポイント:** `GET /v1/pdapi/techs/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Techs.Read`

## 目的

プレーヤーのテクノロジー情報をリストします。テクノロジー識別子は、[paldeck.cc/technology](https://paldeck.cc/technology) で検索できます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` |ターゲット プレーヤー、プレーヤー アカウント、テクノロジー データ、またはテクノロジー テーブルを解決できませんでした。 |
| `500` | `REQUEST_TIMEOUT` |内部ゲーム スレッド コールバックは 5 秒以内に完了しませんでした。 |

## 例

### ユーザーIDごとにロック解除された技術を読み取る

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### PlayerUID によるロック解除されたテクノロジーの読み取り

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## シナリオ

- プレイヤーが [`TechID`](https://paldeck.cc/technology) をすでに持っているかどうかを、学習したり忘れたりする前に確認してください。
- ロックされていないテクノロジーと利用可能なテクノロジーを区別する管理ページを構築します。
- サポートアクション後の進行状況を監査します。
