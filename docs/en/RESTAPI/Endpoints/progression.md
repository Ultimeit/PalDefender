# GET /progression/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/progression/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Progression.Read`

## Purpose

Reads player progression values such as EXP, level-related state, Lifmunk Effigies, and technology point totals.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

No request body.

## Response schema

--8<-- "_snippets/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` | The target player, account, individual character data, record data, or technology data could not be resolved. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |

## Examples

### Read progression by PS5 UserID

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### Read progression by PlayerUID

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Scenarios

- Confirm the current values before granting progression.
- Verify a support action after [POST /give/progression](give-progression.md).
- Build a player overview panel in a trusted admin dashboard.
