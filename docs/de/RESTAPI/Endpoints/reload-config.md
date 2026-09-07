# POST /ReloadConfig



**Endpunkt:** `POST /v1/pdapi/ReloadConfig`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Reload.Config`

## Zweck

Lädt die PalDefender-Konfiguration neu, ohne einen vollständigen Serverneustart zu erfordern.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

Optionales leeres JSON-Objekt.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/reload-config.md"

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

### Konfiguration neu laden

```http
POST /v1/pdapi/ReloadConfig
```

### Nach Tokenänderungen neu laden

```http
POST /v1/pdapi/ReloadConfig
```

## Szenarien

- Änderungen an unterstützten Konfigurationsdateien anwenden.
- Nach Änderungen an `Banlist.json`, Importregeln oder anderen zur Laufzeit lesbaren PalDefender-Dateien neu laden.
- Wenn eine Änderung nach dem Neuladen nicht wirksam wird, starte den Server während eines Wartungsfensters neu.
