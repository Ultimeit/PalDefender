# GET /player/{プレイヤー識別子}



**エンドポイント:** `GET /v1/pdapi/player/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Player.Read`

## 目的

プレイヤー 1 人を返します。識別子は、`UserId` や `PlayerUID` など、サポートされているプレーヤー識別子にすることができます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/player.md"

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
| `404` | `PLAYER_NOT_FOUND` |指定された `player_identifier` と一致するオンライン プレーヤーはありませんでした。 |
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` |プレーヤーは見つかりましたが、プレーヤーのアカウント データをロードできませんでした。 |

## 例

### Steam ユーザー ID による検索

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### PlayerUID による検索

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## シナリオ

- `GET /players` から行を選択した後、プレーヤーの詳細ページを開きます。
・報酬を与えたり罰を与えたりする前に、対象を確認してください。
- プレーヤーが現在サーバーによって解決できるかどうかを確認します。
