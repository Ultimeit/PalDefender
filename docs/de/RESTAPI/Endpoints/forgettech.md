# POST /forgettech/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/forgettech/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Techs.Forget`

## Purpose

Forgets one, many, or all technologies for a player.

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

### Forget one technology for a GDK player

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Forget several technologies by PlayerUID

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Forget all technologies for a Steam player

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Scenarios

- Remove a technology granted by mistake.
- Reset a test account with `"All"`.
- Confirm the current state with [GET /techs](techs.md) before and after the request.
