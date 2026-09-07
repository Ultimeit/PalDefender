### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Version` | object | PalDefender 版本详情。 |

`Version` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Major` | integer | 主版本号。 |
| `Minor` | integer | 次版本号。 |
| `Patch` | integer | 补丁版本号。 |
| `Build` | integer | 构建编号。 |
| `Version` | string | 短版本字符串。 |
| `VersionLong` | string | 长版本字符串。 |
| `Beta` | boolean | 此构建是否标记为测试版。 |
