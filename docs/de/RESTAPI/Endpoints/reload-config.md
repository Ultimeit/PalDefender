# POST /ReloadConfig



**Endpunkt:** `POST /v1/pdapi/ReloadConfig`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Reload.Config`

## Zweck

Reloads PalDefender configuration without requiring a full server restart.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

Optionales leeres JSON-Objekt.

## Antwortschema

--8<-- "_snippets/restapi/schemas/reload-config.md"

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

### Reload configuration

```http
POST /v1/pdapi/ReloadConfig
```

### Reload after token changes

```http
POST /v1/pdapi/ReloadConfig
```

## Szenarien

- Apply edits to supported configuration files.
- Reload after updating `Banlist.json`, import rules, or other runtime-readable PalDefender files.
- Wenn eine Änderung nach dem Neuladen nicht wirksam wird, starte den Server während eines Wartungsfensters neu.
