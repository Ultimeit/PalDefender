# POST /learntech/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/learntech/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Techs.Learn`

## Purpose

Learns one, many, or all technologies for a player.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

`Technology` can be a single [`TechID`](https://paldeck.cc/technology), the string `"All"`, or an array of [`TechID`](https://paldeck.cc/technology) strings. Do not put `"All"` inside an array.

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
| `400` | `INVALID_REQUEST` | `Technology` is missing, or it is not a string/array in the expected format. |
| `400` | `VALIDATION_FAILED` | The `Technology` array contains a non-string, `All`, or an invalid technology identifier. |

## Examples

### Learn one technology for a Steam player

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Learn several technologies for a PS5 player

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Learn every technology by PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Scenarios

- Unlock a missing recipe for support.
- Unlock all technologies for test accounts.
- Validate technology IDs at [paldeck.cc/technology](https://paldeck.cc/technology) before sending the request.
