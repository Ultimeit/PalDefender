# GET /items/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/items/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Items.Read`

## Purpose

Lists the target player's items. Item identifiers in responses can be searched on [paldeck.cc/items](https://paldeck.cc/items).

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
| `400` | `REQUEST_FAILED` | The target player, player state, inventory data, or common inventory container could not be resolved. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |

## Examples

### Read inventory for a Steam player

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### Read inventory for a GDK player

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## Scenarios

- Check inventory before giving compensation.
- Confirm an [`ItemID`](https://paldeck.cc/items) before using [POST /give/items](give-items.md).
- Troubleshoot reports about missing items.
