# POST /SendPlayerMessage

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/SendPlayerMessage`

**Auth:** Bearer token

**Permission:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## Purpose

Sends a message to one or more target players.

## Path parameters

None.

## Query parameters

None.

## Request body

JSON object with `SendType`, `Message`, and either `UserID` or `UserIDs`. Optional `Sender` sets the displayed sender where supported. Common `SendType` values include `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant`, and `PlayerLogVeryImportant`.

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
| `400` | `EMPTY_BODY` | The request body is empty. |
| `400` | `INVALID_JSON` | The request body is not valid JSON. |
| `400` | `VALIDATION_FAILED` | `SendType`, `Message`, `UserID`, or `UserIDs` is missing, empty, duplicated, or has the wrong type. |
| `400` | `PLAYER_NOT_FOUND` | One or more target user IDs or player UIDs could not be found. |
| `400` | `SEND_MESSAGE_FAILED` | Validation passed, but the server rejected the message send operation. |
| `400` | `REQUEST_FAILED` | The game-thread callback threw an exception. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |

## Examples

### Send player chat to one user

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived.",
    "Sender": "Admin"
}
```

### Send important log to mixed targets

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "The event starts in 10 minutes."
}
```

## Scenarios

- Send direct restart warnings to selected players.
- Send support replies from an admin panel.
- Use `UserID` for one target and `UserIDs` for multiple targets, not both.
