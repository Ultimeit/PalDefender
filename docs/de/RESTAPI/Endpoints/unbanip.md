# POST /unbanip/{ip}



**Endpunkt:** `POST /v1/pdapi/unbanip/<ip>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Punishments.UnbanIP`

## Zweck

Unbans an IP address in `Banlist.json`.

## Pfadparameter

- `ip`: IP address to unban.

## Query-Parameter

Keine.

## Request-Body

Optionales JSON-Feld: `Reason` als String.

## Antwortschema

--8<-- "_snippets/restapi/schemas/unbanip.md"

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
| `400` | `VALIDATION_FAILED` | An optional request field has the wrong JSON type. |
| `404` | `BAN_NOT_FOUND` | Die angegebene `ip` ist nicht aktiv gebannt. |

## Beispiele

### Unban an IP with reason

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Temporary block expired"
}
```

### Unban an IP with default reason

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## Szenarien

- Remove an IP ban after investigation.
- Nutzen, wenn ein Spieler nach einem User-Unban weiterhin blockiert ist, weil der IP-Eintrag noch aktiv ist.
- Nutze [GET /banlist](banlist.md) mit `ip`, um das Ergebnis zu prüfen.
