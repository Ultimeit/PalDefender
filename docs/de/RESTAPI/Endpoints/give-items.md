# POST /give/items/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/give/items/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Items.Give`

## Zweck

Gibt dem Zielspieler ein oder mehrere Items.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit `Items`, einem Array von Item-Vergaben. Jeder Eintrag benötigt eine [`ItemID`](https://paldeck.cc/items) und einen positiven `Count`.

## Antwortschema

--8<-- "_snippets/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` | Der Body enthält kein `Items`-Array. |
| `400` | `VALIDATION_FAILED` | One or more item grants are invalid, unsupported, too large, or do not fit in inventory. |
| `500` | `GRANT_FAILED` | Validation passed, but the server failed while adding items to the inventory. |

## Beispiele

### Munition und einen Launcher an einen Steam-Spieler geben

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### Waehrung an einen PS5-Spieler geben

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## Szenarien

- Für Entschädigungspakete nach einem Rollback nutzen.
- Für Shop-Integrationen nutzen, bei denen ein vertrauenswürdiger Dienst gekaufte Items vergibt.
- Validate the [`ItemID`](https://paldeck.cc/items) first; display names are not always valid IDs.
