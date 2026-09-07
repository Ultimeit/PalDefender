# GET /techs/{player_identifier}



**Endpunkt:** `GET /v1/pdapi/techs/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Techs.Read`

## Zweck

Listet Technologieinformationen eines Spielers auf. Technologie-IDs können auf [paldeck.cc/technology](https://paldeck.cc/technology) gesucht werden.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | Zielspieler, Player Account, Technologiedaten oder Technologietabelle konnten nicht aufgeloest werden. |
| `500` | `REQUEST_TIMEOUT` | Der interne Game-Thread-Callback wurde nicht innerhalb von 5 Sekunden abgeschlossen. |

## Beispiele

### Freigeschaltete Technologien anhand der UserID lesen

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### Freigeschaltete Technologien anhand der PlayerUID lesen

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## Szenarien

- Vor dem Freischalten oder Entfernen prüfen, ob ein Spieler eine [`TechID`](https://paldeck.cc/technology) bereits besitzt.
- Eine Adminseite erstellen, die freigeschaltete und verfügbare Technologien trennt.
- Den Fortschritt nach Supportmaßnahmen prüfen.
