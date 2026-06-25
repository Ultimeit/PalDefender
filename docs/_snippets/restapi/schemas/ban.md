### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Success` | boolean | `true` when the ban was recorded. |
| `UserId` | string | User ID that was banned. |
| `IP` | boolean | Whether the request also banned an IP address. |
| `BannedIP` | string | Banned IP address, or an empty string when no IP was banned. |
| `Kicked` | integer | Number of online players kicked by the ban action. |
