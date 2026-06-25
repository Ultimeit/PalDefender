# POST /banip/{ip}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/banip/<ip>`

**Auth:** Bearer token

**Permission:** `REST.Punishments.BanIP`

## Purpose

Bans an IP address and records it in `Banlist.json`.

## Path parameters

- `ip`: IP address to ban.

## Query parameters

None.

## Request body

Optional JSON fields: `Reason` string and `UserId` string when the IP ban should be associated with a user.

## Response schema

--8<-- "_snippets/restapi/schemas/banip.md"

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

## Examples

### Ban an IP only

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Bot traffic"
}
```

### Ban an IP and attach a GDK user

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Alt account abuse",
    "UserId": "gdk_2533274898765432"
}
```

## Scenarios

- Stop repeated abuse from the same IP after staff review.
- Associate `UserId` when known so the banlist is easier to audit.
- Use [GET /banlist](banlist.md) with `ip` to verify the active record.
