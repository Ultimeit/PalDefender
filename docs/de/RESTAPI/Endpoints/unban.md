# POST /unban/{user_id}



**Endpunkt:** `POST /v1/pdapi/unban/<user_id>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Punishments.Unban`

## Zweck

Unbans a user ID in `Banlist.json`.

## Pfadparameter

- `user_id`: User ID to unban.

## Query-Parameter

Keine.

## Request-Body

Optionales JSON-Feld: `Reason` als String.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/unban.md"

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
| `400` | `VALIDATION_FAILED` | Ein optionales Anfragefeld besitzt den falschen JSON-Typ. |
| `404` | `BAN_NOT_FOUND` | Die angegebene `user_id` ist nicht aktiv gebannt. |

## Beispiele

### Einen Steam-Benutzer entsperren

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### Einen PS5-Benutzer mit Standardbegründung entsperren

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## Szenarien

- Eine Benutzersperre nach genehmigtem Einspruch aufheben.
- Eine Begründung für die Prüfspur festhalten.
- Nutze [GET /banlist](banlist.md) mit `userId` oder `q`, um das Ergebnis zu prüfen.
