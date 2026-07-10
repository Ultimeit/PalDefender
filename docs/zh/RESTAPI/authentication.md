# 认证与设置

## 启用 API

1. 打开：`Win64/PalDefender/RESTAPI/RESTConfig.json`
2. 将 `"Enabled"` 设置为 `true`
3. 重启服务器。

启动时你应该看到类似日志：
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Loaded 1 Bearer token.
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Port

- **默认端口：** `17993`

**不要公开暴露。** 如果你需要从局域网/本机之外访问 API，请将它放在 **反向代理**（nginx / Caddy / Traefik）后面，并在那里终止 TLS。实际的 PalDefender REST API 应绑定到 localhost 或私有网络接口。

## Tokens

- 启动服务器一次以生成示例令牌。
- `Win64/PalDefender/RESTAPI/Tokens/` 中的每个 `.json` 文件都会被视为有效令牌文件。（唯一例外是 `TokenExample.json`！）
- 为**每个人/服务**创建一个令牌。令牌就是密码。

令牌文件示例:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

    `Permissions` 可以是字符串，也可以是字符串数组。面向公开仪表盘或自动化时，请使用更窄的权限，避免授予完整管理员访问权。

## Headers
通过标准 Authorization 头发送令牌:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python 示例
```py
import requests

base_url = "http://127.0.0.1:17993"
# 不要这样做。不要把真实令牌存进代码。请使用 .env 等方式！这里只是演示。
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
