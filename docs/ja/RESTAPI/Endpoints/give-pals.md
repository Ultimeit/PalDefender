# POST /give/pals/{player_identifier}



**エンドポイント:** `POST /v1/pdapi/give/pals/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.Pals.Give`

## 目的

ID とレベル別に 1 つ以上の Pals を指定します。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と `Pals`、Pal の array が付与されます。各エントリには [`PalID`](https://paldeck.cc/pals) と正の `Level` が必要です。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` |本体には `Pals` array が含まれていません。 |
| `400` | `VALIDATION_FAILED` | 1 つ以上の Pal 付与が無効であるか、プレーヤーに Pal ストレージ容量が不足しています。 |

## 例

### GDK プレーヤーにスターター Pal を与える

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### PlayerUID でイベント Pals を与える

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## シナリオ

- テンプレート ファイルを維持せずに、単純な Pal 報酬を与えます。
- `PalID` と `Level` のみが異なるランダムな報酬スクリプトに使用します。
- プレーヤーが見つからない場合、[`PalID`](https://paldeck.cc/pals) が無効である場合、または十分な Pal ストレージ容量がない場合、リクエストは失敗する可能性があります。
