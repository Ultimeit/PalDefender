# GET /pals/{プレイヤー識別子}



**エンドポイント:** `GET /v1/pdapi/pals/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Pals.Read`

## 目的

ターゲットプレイヤーのPalsをリストします。応答内の Pal 識別子は、[paldeck.cc/pals](https://paldeck.cc/pals) で検索できます。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/pals.md"

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
| `404` | `PLAYER_STATE_NOT_FOUND` |プレーヤーは存在しますが、`APalPlayerState` は利用できませんでした。 |

## 例

### PS5 プレーヤーの場合は Pals を読んでください

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### PlayerUID で Pals を読み取る

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## シナリオ

- サポートアクションの前にプレーヤーを確認します。
- [POST /give/pals](give-pals.md) または [POST /give/paltemplate](give-paltemplate.md) を使用して、報酬 Pal が到着したことを確認します。
- 欠落している、または予期しない Pals に関するレポートを調査します。
