# POST /learntech/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/learntech/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Techs.Learn`

## Zweck

Learns one, many, or all technologies for a player.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

`Technology` can be a single [`TechID`](https://paldeck.cc/technology), the string `"All"`, or an array of [`TechID`](https://paldeck.cc/technology) strings. Do not put `"All"` inside an array.

## Antwortschema

--8<-- "_snippets/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` is missing, or it is not a string/array in the expected format. |
| `400` | `VALIDATION_FAILED` | The `Technology` array contains a non-string, `All`, or an invalid technology identifier. |

## Beispiele

### Learn one technology for a Steam player

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Learn several technologies for a PS5 player

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Learn every technology by PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Szenarien

- Unlock a missing recipe for support.
- Unlock all technologies for test accounts.
- Validate technology IDs at [paldeck.cc/technology](https://paldeck.cc/technology) before sending the request.
