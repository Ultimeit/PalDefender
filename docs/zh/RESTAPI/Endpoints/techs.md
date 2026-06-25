# GET /techs/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/techs/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Techs.Read`

## Purpose

Lists technology information for a player. Technology identifiers can be searched on [paldeck.cc/technology](https://paldeck.cc/technology).

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

No request body.

## Response schema

--8<-- "_snippets/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | The target player, player account, technology data, or technology table could not be resolved. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |

## Examples

### Read unlocked techs by UserID

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### Read unlocked techs by PlayerUID

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## Scenarios

- Check whether a player already has a [`TechID`](https://paldeck.cc/technology) before learning or forgetting it.
- Build an admin page that separates unlocked and available technologies.
- Audit progression after support actions.
