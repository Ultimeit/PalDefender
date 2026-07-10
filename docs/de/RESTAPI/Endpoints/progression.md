# GET /progression/{player_identifier}



**Endpunkt:** `GET /v1/pdapi/progression/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Progression.Read`

## Zweck

Liest Fortschrittswerte eines Spielers wie EXP, levelbezogenen Status, Reliktsummen und Technologiepunkte.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` | Zielspieler, Account, individuelle Charakterdaten, Record-Daten oder Technologiedaten konnten nicht aufgeloest werden. |
| `500` | `REQUEST_TIMEOUT` | Der interne Game-Thread-Callback wurde nicht innerhalb von 5 Sekunden abgeschlossen. |

## Beispiele

### Read progression by PS5 UserID

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### Read progression by PlayerUID

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Szenarien

- Confirm the current values before granting progression.
- Verify a support action after [POST /give/progression](give-progression.md).
- Build a player overview panel in a trusted admin dashboard.
