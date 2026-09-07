# GET /pals/{player_identifier}



**Endpunkt:** `GET /v1/pdapi/pals/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Pals.Read`

## Zweck

Listet die Pals des Zielspielers. Pal-Identifier aus Antworten können auf [paldeck.cc/pals](https://paldeck.cc/pals) gesucht werden.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/pals.md"

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
| `404` | `PLAYER_NOT_FOUND` | Kein Online-Spieler entsprach dem angegebenen `player_identifier`. |
| `404` | `PLAYER_STATE_NOT_FOUND` | Der Spieler existiert, aber sein `APalPlayerState` war nicht verfügbar. |

## Beispiele

### Pals eines PS5-Spielers lesen

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### Pals anhand der PlayerUID lesen

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## Szenarien

- Einen Spieler vor Supportmaßnahmen prüfen.
- Nach [POST /give/pals](give-pals.md) oder [POST /give/paltemplate](give-paltemplate.md) bestätigen, dass der Belohnungs-Pal angekommen ist.
- Meldungen über fehlende oder unerwartete Pals untersuchen.
