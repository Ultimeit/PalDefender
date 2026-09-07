# POST /forgettech/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/forgettech/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Techs.Forget`

## Zweck

Entfernt eine, mehrere oder alle erlernten Technologien eines Spielers.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

`Technology` kann eine einzelne [`TechID`](https://paldeck.cc/technology), die Zeichenfolge `"All"` oder ein Array aus [`TechID`](https://paldeck.cc/technology)-Zeichenfolgen sein. `"All"` darf nicht innerhalb eines Arrays stehen.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/forgettech.md"

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

### Eine Technologie eines GDK-Spielers entfernen

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Mehrere Technologien anhand der PlayerUID entfernen

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

### Alle Technologien eines Steam-Spielers entfernen

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Szenarien

- Eine versehentlich gewährte Technologie entfernen.
- Ein Testkonto mit `"All"` zurücksetzen.
- Den aktuellen Zustand vor und nach der Anfrage mit [GET /techs](techs.md) prüfen.
