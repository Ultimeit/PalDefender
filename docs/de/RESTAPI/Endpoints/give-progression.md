# POST /give/progression/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/give/progression/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Progression.Give`

## Zweck

Gewährt einem Spieler Fortschrittswerte.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit mindestens einer unterstützten Vergabe: positive Ganzzahl `EXP`, positive Ganzzahl `TechnologyPoints`, positive Ganzzahl `AncientTechnologyPoints` oder `Relics` als nicht leeres Objekt, das Relikt-Typen positive Ganzzahlen zuordnet.


Unterstützte Relikt-Typen: `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## Antwortschema

--8<-- "_snippets/restapi/schemas/give-progression.md"

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
| `400` | `INVALID_REQUEST` | Der Body enthält keines der Felder `EXP`, `Relics`, `TechnologyPoints` oder `AncientTechnologyPoints`. |
| `400` | `VALIDATION_FAILED` | Ein angegebener Fortschrittswert fehlt, ist keine Ganzzahl, ist nicht positiv oder benötigte Fortschrittsdaten sind nicht verfügbar. |

## Beispiele

### EXP an einen GDK-Spieler geben

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### Punkte und Relikte per PlayerUID geben

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## Szenarien

- Kompensiere Spieler nach einem Save-Rollback.
- Füge Technologiepunkte hinzu, ohne eine bestimmte Technologie freizuschalten.
- Nutze stattdessen [POST /learntech](learntech.md), wenn du eine bestimmte [`TechID`](https://paldeck.cc/technology) freischalten willst.
