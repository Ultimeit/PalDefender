# POST /Alert

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/Alert`

**Auth:** Bearer token

**Permission:** `REST.Messages.Alert`

## Purpose

Sends an alert message to the server.

## Path parameters

None.

## Query parameters

None.

## Request body

JSON object with `Message` string.

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
| `400` | `BROADCAST_ALERT_FAILED` | The server failed to send the alert message. |

## Examples

### Send restart alert

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Restart now."
}
```

### Send multiline alert

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Server restart in 5 minutes.\nPlease return to base."
}
```

## Scenarios

- Send high-priority server warnings.
- Use after a broadcast when players need a final urgent notice.
- Keep alerts short so they are readable in-game.
