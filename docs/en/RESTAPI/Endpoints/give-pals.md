# POST /give/pals/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/give/pals/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Pals.Give`

## Purpose

Gives one or more Pals by ID and level.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

JSON object with `Pals`, an array of Pal grants. Each entry needs a [`PalID`](https://paldeck.cc/pals) and positive `Level`.

## Response schema

--8<-- "_snippets/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` | The body does not contain a `Pals` array. |
| `400` | `VALIDATION_FAILED` | One or more Pal grants are invalid, or the player has insufficient Pal storage space. |

## Examples

### Give a starter Pal to a GDK player

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### Give event Pals by PlayerUID

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## Scenarios

- Give simple Pal rewards without maintaining a template file.
- Use for random reward scripts that only vary `PalID` and `Level`.
- The request can fail if the player cannot be found, the [`PalID`](https://paldeck.cc/pals) is invalid, or there is not enough Pal storage space.
