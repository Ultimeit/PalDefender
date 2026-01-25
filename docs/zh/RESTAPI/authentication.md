# 认证和设置

## 启用 API

1. 打开：`Win64/PalDefender/RESTAPI/RESTConfig.json`
2. 将 `"Enabled"` 设置为 `true`
3. 重启服务器。

启动时，您应该看到类似以下的日志：
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:28][info] [RESTAPI] Loaded 1 Bearer token.
<...>
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## 端口

- **默认端口：** `17993`

**不要公开暴露它。** 如果您想从 LAN/机器外部访问 API，请将其放在**反向代理**（nginx / Caddy / Traefik）后面，并在那里终止 TLS。将实际的 PalDefender REST API 绑定到 localhost 或私有接口。

## 令牌

- 启动服务器一次以生成示例令牌。
- `Win64/PalDefender/RESTAPI/Tokens/` 内的每个 `.json` 文件都被视为有效令牌文件。（唯一的例外是文件 `TokenExample.json`！）
- **为每个人/服务创建一个令牌**。令牌就是密码。

示例令牌文件：

```json
{
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"
}
```

## 请求头
通过标准 Authorization 请求头发送令牌：
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python 示例
```py
import requests

base_url = "http://127.0.0.1:17993"
# 不要这样做。永远不要在代码中存储令牌。使用类似 .env 的东西！这仅用于演示。
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```