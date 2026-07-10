# POST /forgettech/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/forgettech/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Techs.Forget`

## Zweck

Forgets one, many, or all technologies for a player.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

`Technology` can be a single [`TechID`](https://paldeck.cc/technology), the string `"All"`, or an array of [`TechID`](https://paldeck.cc/technology) strings. Do not put `"All"` inside an array.

## Antwortschema

--8<-- "_snippets/restapi/schemas/forgettech.md"

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

### Forget one technology for a GDK player

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Forget several technologies by PlayerUID

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Forget all technologies for a Steam player

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Szenarien

- Remove a technology granted by mistake.
- Reset a test account with `"All"`.
- Confirm the current state with [GET /techs](techs.md) before and after the request.
