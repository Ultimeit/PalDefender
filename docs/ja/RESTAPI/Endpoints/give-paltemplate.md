# POST /give/paltemplate/{player_identifier}



**エンドポイント:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**認証:** ベアラートークン

**許可:** `REST.PalTemplates.Give`

## 目的

`Pals/Templates/` 内のファイルから 1 つ以上の Pals を提供します。

## パスパラメータ

- `player_identifier`: 対象プレイヤーの `UserId` または `PlayerUID`。

## クエリパラメータ

なし。

## リクエストボディ

JSON object と `PalTemplates`、テンプレート ファイル名の array。わかりやすくするために、`.json` 拡張子が含まれている場合があります。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` |本体には `PalTemplates` array が含まれていません。 |
| `400` | `VALIDATION_FAILED` | 1 つ以上のテンプレート ファイル名が無効であるか、インポートできないか、Pal ストレージに収まりません。 |

## 例

### 1 つのテンプレート Pal を Steam プレーヤーに提供します

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### PS5 プレイヤーにレイド報酬テンプレートを与える

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## シナリオ

- 報酬に特定のスキル、パッシブ、IV、ソウル、ニックネーム、または作業適性値が必要な場合に使用します。
- [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md) を使用して、最初にテンプレートを作成します。
- `Pals/ImportRules/` のインポート ルールは、テンプレートを許可される前にブロックまたは調整できます。
