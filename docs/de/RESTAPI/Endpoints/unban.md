# POST /unban/{user_id}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/unban/<user_id>`

**Auth:** Bearer token

**Permission:** `REST.Punishments.Unban`

## Purpose

Unbans a user ID in `Banlist.json`.

## Path parameters

- `user_id`: User ID to unban.

## Query parameters

None.

## Request body

Optional JSON field: `Reason` string.

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
| `404` | `BAN_NOT_FOUND` | The supplied `user_id` is not actively banned. |

## Examples

### Unban a Steam user

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### Unban a PS5 user with default reason

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## Scenarios

- Remove a user ban after appeal approval.
- Keep a reason for the audit trail.
- Use [GET /banlist](banlist.md) with `userId` or `q` to verify the result.
