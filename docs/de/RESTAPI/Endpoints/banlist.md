# GET /banlist



**Endpunkt:** `GET /v1/pdapi/banlist`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Banlist.Read`

## Zweck

Liest Bann-Eintraege aus der Bannliste. Bannbezogene Daten werden in `Banlist.json` gespeichert, nicht in `Config.json`.

## Pfadparameter

Keine.

## Query-Parameter

- `active`: `true`, `false` oder `1`, um nach dem Aktivstatus zu filtern.
- `entryType`: Nach Bann-Eintragstyp filtern.
- `userId`: Filter by user ID.
- `ip` or `userIP`: Filter by IP address.
- `issuerType`, `issuerName`, `issuerIP`: Nach Aussteller-Metadaten filtern.
- `reason`: Nach dem Begründungstext filtern.
- `q`: Allgemeine Textsuche.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/banlist.md"

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

### Alle Sperreinträge auflisten

```http
GET /v1/pdapi/banlist
```

### Aktive Einträge eines Steam-Benutzers finden

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### Einträge nach IP durchsuchen

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## Szenarien

- Prüfen, ob ein Spieler oder eine IP derzeit gesperrt ist.
- Vor einer Entsperrung nach Grund oder Aussteller suchen.
- Ein Moderations-Dashboard erstellen, das `Banlist.json` über die API liest.

## Related

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), and [POST /unbanip](unbanip.md).
