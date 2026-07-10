# POST /kick/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/kick/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Punishments.Kick`

## Zweck

Kickt einen Online-Spieler, ohne einen Banneintrag zu erstellen.

## Pfadparameter

- `player_identifier`: `UserId`, `PlayerUID`, or another supported player identifier.

## Query-Parameter

Keine.

## Request-Body

Optionales JSON-Feld: `Reason` als String.

## Antwortschema

--8<-- "_snippets/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` | Der Zielspieler ist nicht online oder konnte nicht gefunden werden. |

## Beispiele

### Kick a GDK player with reason

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "AFK in event area"
}
```

### Kick a Steam player with default reason

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## Szenarien

- Remove a player before maintenance.
- Kick a stuck player so they can reconnect.
- Nutze stattdessen [POST /ban](ban.md), wenn der Spieler nicht zurückkehren dürfen soll.
