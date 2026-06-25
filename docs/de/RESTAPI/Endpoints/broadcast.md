# POST /Broadcast

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/Broadcast`

**Auth:** Bearer token

**Permission:** `REST.Messages.Broadcast`

## Purpose

Broadcasts a chat message to the server.

## Path parameters

None.

## Query parameters

None.

## Request body

JSON object with `Message` string and optional `Sender` string.

## Response schema

--8<-- "_snippets/restapi/schemas/broadcast.md"

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
| `400` | `VALIDATION_FAILED` | `Message` is missing, empty, or not a string. |

## Examples

### Broadcast as SYSTEM

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

### Broadcast with sender name

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Sender": "Admin",
    "Message": "World boss event starts now."
}
```

## Scenarios

- Announce scheduled maintenance.
- Send automated event start messages.
- Use [POST /Alert](alert.md) when the message should be an alert instead of normal broadcast chat.
