# POST /learntech/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/learntech/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Techs.Learn`

## Zweck

Schaltet für einen Spieler eine, mehrere oder alle Technologien frei.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

`Technology` kann eine einzelne [`TechID`](https://paldeck.cc/technology), die Zeichenfolge `"All"` oder ein Array aus [`TechID`](https://paldeck.cc/technology)-Zeichenfolgen sein. `"All"` darf nicht innerhalb eines Arrays stehen.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` fehlt oder ist keine Zeichenfolge beziehungsweise kein Array im erwarteten Format. |
| `400` | `VALIDATION_FAILED` | Das `Technology`-Array enthält einen Wert, der keine Zeichenfolge ist, `All` oder eine ungültige Technologiekennung. |

## Beispiele

### Eine Technologie für einen Steam-Spieler freischalten

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Mehrere Technologien für einen PS5-Spieler freischalten

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

### Alle Technologien anhand der PlayerUID freischalten

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Szenarien

- Ein fehlendes Rezept im Rahmen einer Supportmaßnahme freischalten.
- Alle Technologien für Testkonten freischalten.
- Technologie-IDs vor dem Senden der Anfrage auf [paldeck.cc/technology](https://paldeck.cc/technology) prüfen.
