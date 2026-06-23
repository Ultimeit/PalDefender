# POST /deletebase/{base_camp_id}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**Auth:** Bearer token

**Permission:** `REST.Base.Delete`

## Purpose

Deletes a base/camp by its base camp ID. This is a destructive admin action.

## Path parameters

- `base_camp_id`: Base camp identifier, usually copied from guild/base data.

## Query parameters

None.

## Request body

Optional empty JSON object. Confirm the ID before sending the request.

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
| `400` | `INVALID_BASE_CAMP_ID` | The `base_camp_id` path value is not a valid GUID. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | The server could not access `UPalBaseCampManager`. |
| `404` | `BASE_CAMP_NOT_FOUND` | No base camp matched the supplied GUID. |
| `500` | `DELETE_BASE_FAILED` | The base camp was found, but destruction/cleanup failed. |

## Examples

### Delete a base camp by GUID

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### Delete another base camp by GUID

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## Scenarios

- Remove abandoned or broken bases after staff review.
- Use [GET /guilds](guilds.md) and [GET /guild](guild.md) to identify the correct camp before deletion.
- Do not use this endpoint for routine cleanup unless your staff process already verifies ownership and backups.
