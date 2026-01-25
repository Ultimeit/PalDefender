# PalDefender REST API

本节记录了内置的 PalDefender REST API（一个用于**本地/受信任**使用的小型 HTTP 接口）。

- **默认基础 URL：** `http://127.0.0.1:17993`
- **认证：** Bearer token（所有端点都需要）
- **版本端点：** `/v1/pdapi/version`

> 安全提示：**不要**将此端口直接暴露到公共互联网。如果您需要远程访问，请使用反向代理和适当的访问控制。

## 内容
- [认证和设置](authentication.md)
- [端点](endpoints.md)
