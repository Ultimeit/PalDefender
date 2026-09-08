# GET /banlist



**エンドポイント:** `GET /v1/pdapi/banlist`

**認証:** ベアラートークン

**許可:** `REST.Banlist.Read`

## 目的

禁止リストから禁止レコードを読み取ります。禁止関連のデータは、`Config.json` ではなく、`Banlist.json` に保存されます。

## パスパラメータ

なし。

## クエリパラメータ

- `active`: アクティブ状態をフィルタリングするための `true`、`false`、または `1`。
- `entryType`: 禁止エントリ タイプでフィルタリングします。
- `userId`: ユーザー ID でフィルターします。
- `ip` または `userIP`: IP アドレスでフィルターします。
- `issuerType`、`issuerName`、`issuerIP`: 発行者のメタデータでフィルターします。
- `reason`: 理由テキストでフィルターします。
- `q`: 一般的なテキスト検索。

## リクエストボディ

リクエスト本文がありません。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/banlist.md"

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

## 例

### すべての禁止記録をリストする

```http
GET /v1/pdapi/banlist
```

### Steam ユーザーのアクティブなレコードを検索する

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### IP でレコードを検索

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## シナリオ

- プレーヤーまたは IP が現在禁止されているかどうかを確認します。
- 禁止を解除する前に、理由または発行者で検索します。
- `Banlist.json` から API までを読み取るモデレーション ダッシュボードを構築します。

## 関連

- [POST /ban](ban.md)、[POST /unban](unban.md)、[POST /banip](banip.md)、および [POST /unbanip](unbanip.md)。
