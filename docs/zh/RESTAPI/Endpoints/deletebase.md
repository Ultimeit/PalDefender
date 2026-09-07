# POST /deletebase/{base_camp_id}



**端点:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**认证:** Bearer 令牌

**权限:** `REST.Base.Delete`

## 用途

通过 Base Camp ID 删除基地/营地。这是破坏性管理员操作。

## 路径参数

- `base_camp_id`: 基地标识符，通常从公会或基地数据中复制。

## 查询参数

无。

## 请求体

可选的空 JSON 对象。发送请求前请确认 ID。

## 响应结构

--8<-- "_snippets/zh/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | The `base_camp_id` path value is not a valid GUID. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | 服务器无法访问 `UPalBaseCampManager`。 |
| `404` | `BASE_CAMP_NOT_FOUND` | 没有基地与提供的 GUID 匹配。 |
| `500` | `DELETE_BASE_FAILED` | 已找到 Base Camp，但销毁/清理失败。 |

## 示例

### 按 GUID 删除基地

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### 按 GUID 删除另一个基地

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## 使用场景

- 经管理人员审核后移除废弃或损坏的基地。
- 删除前使用 [GET /guilds](guilds.md) 和 [GET /guild](guild.md) 确认正确的营地。
- 除非管理流程已验证所有权和备份，否则不要将此端点用于例行清理。
