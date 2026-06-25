# GET /version

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/version`

**Auth:** Bearer token

**Permission:** `REST.Version.Read`

## Purpose

Use this endpoint as a health check and version check for tools, dashboards, and scripts.

## Path parameters

None.

## Query parameters

None.

## Request body

No request body.

## Response schema

--8<-- "_snippets/restapi/schemas/version.md"

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

## Examples

### Health and version check

```http
GET /v1/pdapi/version
```

## Scenarios

- Use it after configuring the REST API token to confirm authentication works.
- Use it before calling Beta endpoints if your tool needs a minimum PalDefender version.
- Use it for monitoring, because it is the smallest read-only request.
