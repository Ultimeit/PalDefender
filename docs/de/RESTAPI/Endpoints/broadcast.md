# POST /Broadcast



**Endpunkt:** `POST /v1/pdapi/Broadcast`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Messages.Broadcast`

## Zweck

Sendet eine Chatnachricht an den Server.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit dem erforderlichen String `Message`.

## Antwortschema

--8<-- "_snippets/restapi/schemas/broadcast.md"

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
| `400` | `VALIDATION_FAILED` | `Message` fehlt, ist leer oder kein String. |

## Beispiele

### Neustart-Hinweis senden

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

## Szenarien

- Kündige geplante Wartungen an.
- Sende automatische Event-Startmeldungen.
- Nutze [POST /Alert](alert.md), wenn die Nachricht ein Alarm statt normaler Broadcast-Chat sein soll.
