# GET /banlist

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `GET /v1/pdapi/banlist`

**Auth:** Bearer token

**Permission:** `REST.Banlist.Read`

## Purpose

Reads ban records from the ban list. Ban-related data is stored in `Banlist.json`, not `Config.json`.

## Path parameters

None.

## Query parameters

- `active`: `true`, `false`, or `1` to filter active state.
- `entryType`: Filter by ban entry type.
- `userId`: Filter by user ID.
- `ip` or `userIP`: Filter by IP address.
- `issuerType`, `issuerName`, `issuerIP`: Filter by issuer metadata.
- `reason`: Filter by reason text.
- `q`: General text search.

## Request body

No request body.

## Response schema

--8<-- "_snippets/restapi/schemas/banlist.md"

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

### List all ban records

```http
GET /v1/pdapi/banlist
```

### Find active records for a Steam user

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### Search records by IP

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## Scenarios

- Check whether a player or IP is currently banned.
- Search by reason or issuer before unbanning.
- Build a moderation dashboard that reads from `Banlist.json` through the API.

## Related

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), and [POST /unbanip](unbanip.md).
