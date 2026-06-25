# POST /unbanip/{ip}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/unbanip/<ip>`

**Auth:** Bearer token

**Permission:** `REST.Punishments.UnbanIP`

## Purpose

Unbans an IP address in `Banlist.json`.

## Path parameters

- `ip`: IP address to unban.

## Query parameters

None.

## Request body

Optional JSON field: `Reason` string.

## Response schema

--8<-- "_snippets/restapi/schemas/unbanip.md"

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
| `400` | `INVALID_JSON` | A request body was supplied, but it could not be parsed as JSON. |
| `400` | `REQUEST_FAILED` | The game-thread callback threw an exception, or a shared player/resource resolver failed. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |
| `400` | `VALIDATION_FAILED` | An optional request field has the wrong JSON type. |
| `404` | `BAN_NOT_FOUND` | The supplied `ip` is not actively banned. |

## Examples

### Unban an IP with reason

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Temporary block expired"
}
```

### Unban an IP with default reason

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## Scenarios

- Remove an IP ban after investigation.
- Use when a player is still blocked after user-level unban because the IP record remains active.
- Use [GET /banlist](banlist.md) with `ip` to verify the result.
