# POST /learntech/{プレイヤー識別子}



**エンドポイント:** `POST /v1/pdapi/learntech/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Techs.Learn`

## 目的

プレーヤーのために 1 つ、複数、またはすべてのテクノロジーを学習します。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

`Technology` には、単一の [`TechID`](https://paldeck.cc/technology)、string `"All"`、または [`TechID`](https://paldeck.cc/technology) 文字列の array を指定できます。 `"All"` を array の中に入れないでください。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` が欠落しているか、予期される形式の string/array ではありません。 |
| `400` | `VALIDATION_FAILED` | `Technology` array には、string、`All` 以外、または無効なテクノロジ識別子が含まれています。 |

## 例

### Steam プレーヤー向けの 1 つのテクノロジーを学ぶ

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### PS5 プレーヤー向けのいくつかのテクノロジーを学ぶ

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### PlayerUID であらゆるテクノロジーを学ぶ

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## シナリオ

- サポートのために不足しているレシピのロックを解除します。
- テストアカウントのすべてのテクノロジーのロックを解除します。
- リクエストを送信する前に、[paldeck.cc/technology](https://paldeck.cc/technology) でテクノロジー ID を検証してください。
