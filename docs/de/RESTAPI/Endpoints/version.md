# GET /version



**Endpunkt:** `GET /v1/pdapi/version`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Version.Read`

## Zweck

Nutze diesen Endpunkt als Health-Check und Versionsprüfung für Tools, Dashboards und Skripte.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/version.md"

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

### Zustands- und Versionsprüfung

```http
GET /v1/pdapi/version
```

## Szenarien

- Nutze ihn nach dem Konfigurieren des REST-API-Tokens, um die Authentifizierung zu prüfen.
- Nutze ihn vor weiteren Endpunktaufrufen, wenn dein Tool eine Mindestversion von PalDefender benötigt.
- Nutze ihn für Monitoring, da es der kleinste schreibgeschützte Request ist.
