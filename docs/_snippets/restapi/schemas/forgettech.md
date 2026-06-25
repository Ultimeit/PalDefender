### 200 response schema

| Field | Type | Description |
|-------|------|-------------|
| `ForgottenCount` | integer | Number of technologies removed from the player. |
| `Forgotten` | string[] or string | Removed technology IDs, or `All` when every unlocked technology was removed. |
| `Skipped` | string[] | Technology IDs skipped because they were not unlocked. |
