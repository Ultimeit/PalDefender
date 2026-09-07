# POST /give/paleggs/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.PalEggs.Give`

## Zweck

Gibt dem Zielspieler ein oder mehrere Pal-Eier.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit `PalEggs`, einem Array von Ei-Vergaben. `EggID` ist eine [`ItemID`](https://paldeck.cc/items). Jedes Ei muss entweder [`PalID`](https://paldeck.cc/pals) oder `PalTemplate` verwenden, nicht beides.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | Der Body enthält kein `PalEggs`-Array. |
| `400` | `VALIDATION_FAILED` | One or more egg grants are invalid, cannot be imported, or do not fit in inventory. |

## Beispiele

### Ei mit Level an einen Steam-Spieler geben

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### Template-basiertes Ei per PlayerUID geben

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## Szenarien

- Event-Eier vergeben, ohne den Pal sofort zu spawnen.
- Nutze `PalID` für einfache Eier und `PalTemplate` für benutzerdefinierte Ei-Inhalte.
- Die Anfrage kann fehlschlagen, wenn die Ei-[`ItemID`](https://paldeck.cc/items) ungültig ist oder das Inventar des Spielers keinen Platz hat.
