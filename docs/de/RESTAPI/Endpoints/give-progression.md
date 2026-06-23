# POST /give/progression/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/give/progression/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Progression.Give`

## Purpose

Grants progression values to a player.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

JSON object with at least one positive integer field: `EXP`, `Lifmunks`, `TechnologyPoints`, or `AncientTechnologyPoints`.

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
| `400` | `INVALID_REQUEST` | The body does not include any of `EXP`, `Lifmunks`, `TechnologyPoints`, or `AncientTechnologyPoints`. |
| `400` | `VALIDATION_FAILED` | A supplied progression value is missing, non-integer, non-positive, or required progression internals are unavailable. |

## Examples

### Give EXP to a GDK player

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### Give points and Lifmunks by PlayerUID

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Lifmunks": 5,
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## Scenarios

- Compensate players after a save rollback.
- Add technology points without unlocking a specific technology.
- Use [POST /learntech](learntech.md) instead when you want to unlock a specific [`TechID`](https://paldeck.cc/technology).
