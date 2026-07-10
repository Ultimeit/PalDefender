# POST /give/paltemplate/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.PalTemplates.Give`

## Zweck

Gibt einen oder mehrere Pals aus Dateien in `Pals/Templates/`.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit `PalTemplates`, einem Array von Template-Dateinamen. Die Endung `.json` kann zur Klarheit angegeben werden.

## Antwortschema

--8<-- "_snippets/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | Der Body enthält kein `PalTemplates`-Array. |
| `400` | `VALIDATION_FAILED` | One or more template filenames are invalid, cannot be imported, or do not fit in Pal storage. |

## Beispiele

### Einen Template-Pal an einen Steam-Spieler geben

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### Raid-Belohnungs-Templates an einen PS5-Spieler geben

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## Szenarien

- Nutzen, wenn Belohnungen bestimmte Skills, Passives, IVs, Souls, Spitznamen oder Arbeits-Eignungswerte brauchen.
- Erstelle das Template zuerst über [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md).
- Import rules in `Pals/ImportRules/` can block or adjust templates before they are granted.
