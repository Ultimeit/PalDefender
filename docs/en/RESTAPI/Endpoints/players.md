# GET /players

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/players`

**Auth:** Bearer token

**Permission:** `REST.Players.Read`

## Purpose

Lists known players with identifying and status information. Use it to build player selectors for admin tools.

## Path parameters

None.

## Query parameters

None.

## Request body

No request body.

## Response schema

--8<-- "_snippets/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | The server could not access the Palworld player manager. |

## Examples

### List all known players

```http
GET /v1/pdapi/players
```

### Refresh an admin player selector

```http
GET /v1/pdapi/players
```

## Scenarios

- Build a dropdown of online and known players.
- Find the correct `UserId` or `PlayerUID` before calling reward, punishment, or inventory endpoints.
- Audit who is online before sending a message or scheduled maintenance warning.

## Related

- [GET /player](player.md) for one player.
- [POST /kick](kick.md), [POST /ban](ban.md), and reward endpoints use the same player identifier style.
