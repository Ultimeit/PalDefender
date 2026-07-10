# GET /guilds



**Endpunkt:** `GET /v1/pdapi/guilds`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Guilds.Read`

## Zweck

Listet bekannte Gilden mit Zusammenfassung auf. Nutze diesen Endpunkt, um Gilden-IDs zu finden, bevor du eine bestimmte Gilde abfragst.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/restapi/schemas/guilds.md"

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
| `400` | `INVALID_JSON` | Ein Request-Body wurde gesendet, konnte aber nicht als JSON gelesen werden. |
| `400` | `REQUEST_FAILED` | Der Game-Thread-Callback hat eine Ausnahme ausgelöst oder ein gemeinsamer Spieler-/Ressourcen-Resolver ist fehlgeschlagen. |
| `500` | `REQUEST_TIMEOUT` | Der interne Game-Thread-Callback wurde nicht innerhalb von 5 Sekunden abgeschlossen. |

## Beispiele

### List all guilds

```http
GET /v1/pdapi/guilds
```

### Refresh guild dashboard data

```http
GET /v1/pdapi/guilds
```

## Szenarien

- Build a guild selector in an admin panel.
- Find the `guild_id` for [GET /guild](guild.md).
- Audit base counts, member counts, and guild ownership at a glance.
