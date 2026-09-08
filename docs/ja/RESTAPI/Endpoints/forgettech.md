# POST /forgettech/{プレイヤー識別子}



**エンドポイント:** `POST /v1/pdapi/forgettech/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Techs.Forget`

## 目的

プレーヤーの 1 つ、複数、またはすべてのテクノロジーを忘れます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

`Technology` には、単一の [`TechID`](https://paldeck.cc/technology)、string `"All"`、または [`TechID`](https://paldeck.cc/technology) 文字列の array を指定できます。 `"All"` を array の中に入れないでください。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/forgettech.md"

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

### GDK プレーヤーのテクノロジを 1 つ忘れてください

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### PlayerUID によっていくつかのテクノロジーを忘れます

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Steam プレーヤーのテクノロジーをすべて忘れてください

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## シナリオ

- 誤って付与された技術を削除します。
- `"All"` を使用してテスト アカウントをリセットします。
・リクエストの前後で[GET /techs](techs.md)で現在の状態を確認してください。
