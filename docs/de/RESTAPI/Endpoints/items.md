# GET /items/{player_identifier}



**Endpunkt:** `GET /v1/pdapi/items/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Items.Read`

## Zweck

Listet die Items des Zielspielers. Item-Identifier aus Antworten können auf [paldeck.cc/items](https://paldeck.cc/items) gesucht werden.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` | Zielspieler, Player State, Inventardaten oder gemeinsamer Inventarcontainer konnten nicht aufgeloest werden. |
| `500` | `REQUEST_TIMEOUT` | Der interne Game-Thread-Callback wurde nicht innerhalb von 5 Sekunden abgeschlossen. |

## Beispiele

### Inventar eines Steam-Spielers lesen

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### Inventar eines GDK-Spielers lesen

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## Szenarien

- Das Inventar vor einer Entschädigung prüfen.
- Eine [`ItemID`](https://paldeck.cc/items) vor der Verwendung von [POST /give/items](give-items.md) bestätigen.
- Meldungen über fehlende Gegenstände untersuchen.
