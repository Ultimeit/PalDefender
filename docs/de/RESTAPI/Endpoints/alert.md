# POST /Alert



**Endpunkt:** `POST /v1/pdapi/Alert`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Messages.Alert`

## Zweck

Sendet eine Warnmeldung an den Server.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit dem String `Message`.

## Antwortschema

--8<-- "_snippets/restapi/schemas/alert.md"

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
| `400` | `BROADCAST_ALERT_FAILED` | Der Server konnte die Warnmeldung nicht senden. |

## Beispiele

### Neustart-Warnung senden

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Restart now."
}
```

### Mehrzeilige Warnung senden

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Server restart in 5 minutes.\nPlease return to base."
}
```

## Szenarien

- Sende wichtige Serverwarnungen.
- Nutze dies nach einer Broadcast-Nachricht, wenn Spieler einen letzten dringenden Hinweis benötigen.
- Halte Warnungen kurz, damit sie im Spiel lesbar bleiben.
