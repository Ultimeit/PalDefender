# POST /give/items/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/give/items/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Items.Give`

## Purpose

Gives one or more items to the target player.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

JSON object with `Items`, an array of item grants. Each entry needs an [`ItemID`](https://paldeck.cc/items) and positive `Count`.

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
| `400` | `INVALID_REQUEST` | The body does not contain an `Items` array. |
| `400` | `VALIDATION_FAILED` | One or more item grants are invalid, unsupported, too large, or do not fit in inventory. |
| `500` | `GRANT_FAILED` | Validation passed, but the server failed while adding items to the inventory. |

## Examples

### Give ammo and a launcher to a Steam player

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### Give currency to a PS5 player

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## Scenarios

- Use for compensation packages after a rollback.
- Use for shop integrations where a trusted service grants purchased items.
- Validate the [`ItemID`](https://paldeck.cc/items) first; display names are not always valid IDs.
