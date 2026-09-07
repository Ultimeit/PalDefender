# POST /ReloadConfig



**端点:** `POST /v1/pdapi/ReloadConfig`

**认证:** Bearer 令牌

**权限:** `REST.Reload.Config`

## 用途

无需完整重启服务器即可重新加载 PalDefender 配置。

## 路径参数

无。

## 查询参数

无。

## 请求体

可选的空 JSON 对象。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/reload-config.md"

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

## 示例

### 重新加载配置

```http
POST /v1/pdapi/ReloadConfig
```

### Token 更改后重新加载

```http
POST /v1/pdapi/ReloadConfig
```

## 使用场景

- 应用对受支持配置文件的修改。
- 更新 `Banlist.json`、导入规则或其他运行时可读取的 PalDefender 文件后重新加载。
- 如果更改在重新加载后没有生效，请在维护窗口期间重启服务器。
