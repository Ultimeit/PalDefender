# GET /guild/{guild_id}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/guild/<guild_id>`

**Auth:** Bearer token

**Permission:** `REST.Guild.Read`

## Purpose

Returns one guild with detailed member and base/camp information.

## Path parameters

- `guild_id`: Guild identifier, usually copied from [GET /guilds](guilds.md).

## Query parameters

None.

## Request body

No request body.

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
| `404` | `GUILD_NOT_FOUND` | No guild matched the supplied `guild_id`. |

## Examples

### Read guild roster and camps

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### Read another guild by GUID

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Scenarios

- Investigate base ownership before deleting a base.
- Review guild members and camp data for support requests.
- Use camp IDs from the response carefully with [POST /deletebase](deletebase.md).
