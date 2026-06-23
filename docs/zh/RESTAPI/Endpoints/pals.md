# GET /pals/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/pals/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Pals.Read`

## Purpose

Lists the target player's Pals. Pal identifiers in responses can be searched on [paldeck.cc/pals](https://paldeck.cc/pals).

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

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
| `404` | `PLAYER_NOT_FOUND` | No online player matched the supplied `player_identifier`. |
| `404` | `PLAYER_STATE_NOT_FOUND` | The player exists, but their `APalPlayerState` was unavailable. |

## Examples

### Read Pals for a PS5 player

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### Read Pals by PlayerUID

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## Scenarios

- Review a player before support actions.
- Confirm that a reward Pal arrived after using [POST /give/pals](give-pals.md) or [POST /give/paltemplate](give-paltemplate.md).
- Investigate reports about missing or unexpected Pals.
