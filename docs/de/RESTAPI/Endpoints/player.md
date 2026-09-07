# GET /player/{player_identifier}



**Endpunkt:** `GET /v1/pdapi/player/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Player.Read`

## Zweck

Gibt einen Spieler zurück. Der Identifier kann ein unterstützter Spieler-Identifier wie `UserId` oder `PlayerUID` sein.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/player.md"

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
| `404` | `PLAYER_NOT_FOUND` | Kein Online-Spieler entsprach dem angegebenen `player_identifier`. |
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | Der Spieler wurde gefunden, aber die Player-Account-Daten konnten nicht geladen werden. |

## Beispiele

### Abfrage anhand der Steam-UserID

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### Lookup by PlayerUID

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## Szenarien

- Öffne eine Spieler-Detailseite, nachdem du eine Zeile aus `GET /players` ausgewählt hast.
- Das Ziel vor der Vergabe von Belohnungen oder Anwendung von Strafen bestätigen.
- Prüfen, ob der Spieler derzeit vom Server aufgelöst werden kann.
