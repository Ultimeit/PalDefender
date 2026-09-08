# 認証とセットアップ

## API の有効化

1. `Win64/PalDefender/RESTAPI/RESTConfig.json` を開きます。
2. `"Enabled"` を `true` に設定します
3. サーバーを再起動します。

起動時に次のようなログが表示されるはずです。
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Loaded 1 Bearer token.
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## ポート

- **デフォルトのポート:** `17993`

**公開しないでください。** LAN/マシンの外部から API にアクセスしたい場合は、**リバース プロキシ** (nginx / Caddy / Traefik) の背後に配置し、そこで TLS を終了します。実際の PalDefender REST API をローカルホストまたはプライベート インターフェイスにバインドしたままにしておきます。

## トークン

- サーバーを 1 回起動して、サンプル トークンを生成します。
- `Win64/PalDefender/RESTAPI/Tokens/` 内のすべての `.json` ファイルは、有効なトークン ファイルとして扱われます。 (唯一の例外はファイル `TokenExample.json` です!)
- **1 人あたり 1 つのトークン**を作成します。トークンはパスワードです。

トークンファイルの例:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

    `Permissions` には、単一の string または string の array を指定できます。完全な管理者権限を必要としない公開ダッシュボードや自動処理には、必要最小限の権限を設定してください。

## ヘッダー
標準の Authorization ヘッダーを介してトークンを送信します。
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python の例
```py
import requests

base_url = "http://127.0.0.1:17993"
# do not do this. Never store the token in any code. use smth like .env! This is only for demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
