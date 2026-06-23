# POST /give/paleggs/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.PalEggs.Give`

## Purpose

Gives one or more Pal eggs to the target player.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

JSON object with `PalEggs`, an array of egg grants. `EggID` is an [`ItemID`](https://paldeck.cc/items). Each egg must use either [`PalID`](https://paldeck.cc/pals) or `PalTemplate`, not both.

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
| `400` | `INVALID_REQUEST` | The body does not contain a `PalEggs` array. |
| `400` | `VALIDATION_FAILED` | One or more egg grants are invalid, cannot be imported, or do not fit in inventory. |

## Examples

### Give a leveled egg to a Steam player

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### Give template-backed egg by PlayerUID

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## Scenarios

- Give event eggs without spawning the Pal immediately.
- Use `PalID` for simple eggs and `PalTemplate` for custom egg contents.
- The request can fail if the egg [`ItemID`](https://paldeck.cc/items) is invalid or the player inventory has no space.
