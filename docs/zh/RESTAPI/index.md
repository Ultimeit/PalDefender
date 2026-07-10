# PalDefender REST API

本节记录内置的 PalDefender REST API。这是一个用于**本地 / 受信任**环境的小型 HTTP 接口。

- **默认基础 URL:** `http://127.0.0.1:17993`
- **认证:** Bearer 令牌 (所有端点都需要)
- **版本端点:** `/v1/pdapi/version`

> 安全提示：不要将此端口直接暴露到公网。如果需要远程访问，请使用反向代理并配置合适的访问控制。

## 本节内容
- [认证与设置](authentication.md)
- [端点](Endpoints/index.md)
