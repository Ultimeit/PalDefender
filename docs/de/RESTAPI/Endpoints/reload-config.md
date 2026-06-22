# POST /ReloadConfig

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/ReloadConfig`

**Auth:** Bearer token

**Permission:** `REST.Reload.Config`

## Purpose

Reloads PalDefender configuration without requiring a full server restart.

## Path parameters

None.

## Query parameters

None.

## Request body

Optional empty JSON object.

## Error responses

Error bodies use this shape:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP | Error code | When it happens |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | The `Authorization` header is missing, malformed, or does not match a configured bearer token. |
| `403` | `MISSING_PERMISSION` | The token is valid, but it does not include this endpoint permission. |

## Examples

### Reload configuration

```http
POST /v1/pdapi/ReloadConfig
```

### Reload after token changes

```http
POST /v1/pdapi/ReloadConfig
```

## Scenarios

- Apply edits to supported configuration files.
- Reload after updating `Banlist.json`, import rules, or other runtime-readable PalDefender files.
- If a change does not take effect after reload, restart the server during a maintenance window.
