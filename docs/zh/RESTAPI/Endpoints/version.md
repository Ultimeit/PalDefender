# GET /version



**端点:** `GET /v1/pdapi/version`

**认证:** Bearer 令牌

**权限:** `REST.Version.Read`

## 用途

将此端点用作工具、仪表盘和脚本的健康检查与版本检查。

## 路径参数

无。

## 查询参数

无。

## 请求体

无请求体。

## 响应结构

--8<-- "_snippets/restapi/schemas/version.md"

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

### Health and version check

```http
GET /v1/pdapi/version
```

## 使用场景

- 配置 REST API 令牌后使用它确认认证是否正常。
- 如果工具需要最低 PalDefender 版本，请在调用其他端点前使用它。
- 可用于监控，因为它是最小的只读请求。
