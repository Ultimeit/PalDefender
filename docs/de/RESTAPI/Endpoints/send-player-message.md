# POST /SendPlayerMessage



**Endpunkt:** `POST /v1/pdapi/SendPlayerMessage`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## Zweck

Sendet eine Nachricht an einen oder mehrere Zielspieler.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit `SendType`, `Message` und entweder `UserID` oder `UserIDs`. Gängige `SendType`-Werte sind `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant` und `PlayerLogVeryImportant`.

## Antwortschema

--8<-- "_snippets/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` | Der Request-Body ist leer. |
| `400` | `INVALID_JSON` | Der Request-Body ist kein gültiges JSON. |
| `400` | `VALIDATION_FAILED` | `SendType`, `Message`, `UserID` oder `UserIDs` fehlt, ist leer, doppelt vorhanden oder hat den falschen Typ. |
| `400` | `PLAYER_NOT_FOUND` | One or more target user IDs or player UIDs could not be found. |
| `400` | `SEND_MESSAGE_FAILED` | Validation passed, but the server rejected the message send operation. |
| `400` | `REQUEST_FAILED` | Der Game-Thread-Callback hat eine Ausnahme ausgelöst. |
| `500` | `REQUEST_TIMEOUT` | Der interne Game-Thread-Callback wurde nicht innerhalb von 5 Sekunden abgeschlossen. |

## Beispiele

### Spielerchat an einen Benutzer senden

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived."
}
```

### Wichtige Lognachricht an gemischte Ziele senden

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "Das Event startet in 10 Minuten."
}
```

## Szenarien

- Sende direkte Neustartwarnungen an ausgewählte Spieler.
- Sende Support-Antworten aus einem Admin-Panel.
- Nutze `UserID` für ein Ziel und `UserIDs` für mehrere Ziele, nicht beides.
