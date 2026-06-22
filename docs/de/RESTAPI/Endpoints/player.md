# GET /player/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/player/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Player.Read`

## Purpose

Returns one player. The identifier can be a supported player identifier such as `UserId` or `PlayerUID`.

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
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | The player was found, but the player account data could not be loaded. |

## Examples

### Lookup by Steam UserID

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### Lookup by PlayerUID

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## Scenarios

- Open a player detail page after selecting a row from `GET /players`.
- Confirm the target before giving rewards or applying punishments.
- Check whether the player can currently be resolved by the server.
