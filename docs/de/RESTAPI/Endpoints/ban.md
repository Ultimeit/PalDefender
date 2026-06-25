# POST /ban/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/ban/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.Punishments.Ban`

## Purpose

Bans a user and records the ban in `Banlist.json`. The target may be kicked if currently online.

## Path parameters

- `player_identifier`: `UserId`, `PlayerUID`, or another supported player identifier.

## Query parameters

None.

## Request body

Optional JSON fields: `Reason` string and `IP` boolean. Set `IP` to `true` only when you also want to ban the resolved IP address.

## Response schema

--8<-- "_snippets/restapi/schemas/ban.md"

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
| `400` | `IP_UNAVAILABLE` | `IP` was `true`, but the server could not resolve an IP for the target user. |

## Examples

### Ban a Steam user

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Chargeback fraud"
}
```

### Ban a PS5 user and their resolved IP

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Ban evasion",
    "IP": true
}
```

## Scenarios

- Ban a player by `UserId` after moderation review.
- Include a clear reason so future staff can understand the banlist entry.
- Use [GET /banlist](banlist.md) to verify the active record. Ban-related data is no longer managed in `Config.json`.
