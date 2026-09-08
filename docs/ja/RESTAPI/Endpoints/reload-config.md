# POST /ReloadConfig



**エンドポイント:** `POST /v1/pdapi/ReloadConfig`

**認証:** ベアラートークン

**許可:** `REST.Reload.Config`

## 目的

サーバーを完全に再起動することなく、PalDefender 構成をリロードします。

## パスパラメータ

なし。

## クエリパラメータ

なし。

## リクエストボディ

オプションの空の JSON object。

## 応答スキーマ

--8<-- "_snippets/restapi/schemas/reload-config.md"

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

### 設定をリロードする

```http
POST /v1/pdapi/ReloadConfig
```

### トークン変更後のリロード

```http
POST /v1/pdapi/ReloadConfig
```

## シナリオ

- サポートされている構成ファイルに編集を適用します。
- `Banlist.json`、インポート ルール、またはその他のランタイム読み取り可能な PalDefender ファイルを更新した後にリロードします。
- リロードしても変更が有効にならない場合は、メンテナンス期間中にサーバーを再起動します。
