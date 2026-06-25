### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `Success` | boolean | `true` when the IP ban was recorded. |
| `IP` | string | IP address that was banned. |
| `UserId` | string | Optional user ID recorded with the IP ban. |
| `Kicked` | integer | Number of online players kicked from that IP address. |
