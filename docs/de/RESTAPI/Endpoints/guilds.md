# GET /guilds

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/guilds`

**Auth:** Bearer token

**Permission:** `REST.Guilds.Read`

## Purpose

Lists known guilds with summary information. Use this endpoint to discover guild IDs before requesting a specific guild.

## Path parameters

None.

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

## Examples

### List all guilds

```http
GET /v1/pdapi/guilds
```

### Refresh guild dashboard data

```http
GET /v1/pdapi/guilds
```

## Scenarios

- Build a guild selector in an admin panel.
- Find the `guild_id` for [GET /guild](guild.md).
- Audit base counts, member counts, and guild ownership at a glance.
