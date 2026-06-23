# POST /kick/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/kick/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Punishments.Kick`

## Purpose

Kicks an online player without creating a ban record.

## Path parameters

- `player_identifier`: `UserId`, `PlayerUID`, or another supported player identifier.

## Query parameters

None.

## Request body

Optional JSON field: `Reason` string.

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
| `400` | `VALIDATION_FAILED` | An optional request field has the wrong JSON type. |
| `404` | `PLAYER_NOT_FOUND` | The target player is not online or could not be found. |

## Examples

### Kick a GDK player with reason

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "AFK in event area"
}
```

### Kick a Steam player with default reason

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## Scenarios

- Remove a player before maintenance.
- Kick a stuck player so they can reconnect.
- Use [POST /ban](ban.md) instead when the player should not be allowed back.
