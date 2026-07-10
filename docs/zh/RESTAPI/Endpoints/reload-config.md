# POST /ReloadConfig



**端点:** `POST /v1/pdapi/ReloadConfig`

**认证:** Bearer 令牌

**权限:** `REST.Reload.Config`

## 用途

Reloads PalDefender configuration without requiring a full server restart.

## 路径参数

无。

## 查询参数

无。

## 请求体

可选的空 JSON 对象。

## 响应结构

--8<-- "_snippets/restapi/schemas/reload-config.md"

## 错误响应

错误响应使用以下格式:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "人类可读的消息",
        "详情": {}
    }
}
```

| HTTP | 错误代码 | 发生条件 |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` 头缺失、格式错误，或与配置的 Bearer 令牌不匹配。 |
| `403` | `MISSING_PERMISSION` | 令牌有效，但不包含此端点权限。 |

## 示例

### Reload configuration

```http
POST /v1/pdapi/ReloadConfig
```

### Reload after token changes

```http
POST /v1/pdapi/ReloadConfig
```

## 使用场景

- Apply edits to supported configuration files.
- Reload after updating `Banlist.json`, import rules, or other runtime-readable PalDefender files.
- 如果更改在重新加载后没有生效，请在维护窗口期间重启服务器。
