# GET /banlist



**Endpunkt:** `GET /v1/pdapi/banlist`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Banlist.Read`

## Zweck

Liest Bann-Eintraege aus der Bannliste. Bannbezogene Daten werden in `Banlist.json` gespeichert, nicht in `Config.json`.

## Pfadparameter

Keine.

## Query-Parameter

- `active`: `true`, `false`, or `1` to filter active state.
- `entryType`: Nach Bann-Eintragstyp filtern.
- `userId`: Filter by user ID.
- `ip` or `userIP`: Filter by IP address.
- `issuerType`, `issuerName`, `issuerIP`: Nach Aussteller-Metadaten filtern.
- `reason`: Filter by reason text.
- `q`: General text search.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/restapi/schemas/banlist.md"

## Fehlerantworten

Fehlerantworten verwenden dieses Format:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Für Menschen lesbare Nachricht",
        "Details": {}
    }
}
```

| HTTP | Fehlercode | Wann es passiert |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | Der `Authorization`-Header fehlt, ist fehlerhaft oder passt zu keinem konfigurierten Bearer-Token. |
| `403` | `MISSING_PERMISSION` | Das Token ist gültig, enthält aber nicht die Berechtigung für diesen Endpunkt. |

## Beispiele

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

## Szenarien

- Check whether a player or IP is currently banned.
- Search by reason or issuer before unbanning.
- Build a moderation dashboard that reads from `Banlist.json` through the API.

## Related

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), and [POST /unbanip](unbanip.md).
