# POST /banip/{ip}



**端点:** `POST /v1/pdapi/banip/<ip>`

**认证:** Bearer 令牌

**权限:** `REST.Punishments.BanIP`

## 用途

封禁 IP 地址并记录到 `Banlist.json`。

## 路径参数

- `ip`: IP address to ban.

## 查询参数

无。

## 请求体

可选 JSON 字段：字符串 `Reason`；如果此 IP 封禁应关联到某个用户，也可提供字符串 `UserId`。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/banip.md"

## 错误响应

错误响应使用以下格式:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "人类可读的消息",
        "Details": {}
    }
}
```

| HTTP | 错误代码 | 发生条件 |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` 头缺失、格式错误，或与配置的 Bearer 令牌不匹配。 |
| `403` | `MISSING_PERMISSION` | 令牌有效，但不包含此端点权限。 |
| `400` | `INVALID_JSON` | 提供了请求体，但无法解析为 JSON。 |
| `400` | `REQUEST_FAILED` | 游戏线程回调抛出异常，或共享玩家/资源解析器失败。 |
| `500` | `REQUEST_TIMEOUT` | 内部游戏线程回调未在 5 秒内完成。 |
| `400` | `VALIDATION_FAILED` | 可选请求字段的 JSON 类型错误。 |

## 示例

### 仅封禁 IP

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Bot traffic"
}
```

### 封禁 IP 并关联 GDK 用户

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Alt account abuse",
    "UserId": "gdk_2533274898765432"
}
```

## 使用场景

- 经管理人员审核后，阻止来自同一 IP 的重复滥用。
- 已知时关联 `UserId`，以便更轻松地审计封禁列表。
- 使用带 `ip` 的 [GET /banlist](banlist.md) 验证活动记录。
