# GET /players



**Endpunkt:** `GET /v1/pdapi/players`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Players.Read`

## Zweck

Listet bekannte Spieler mit Identifikations- und Statusinformationen. Nutze dies, um Spielerauswahlen für Admin-Tools zu bauen.

## Pfadparameter

Keine.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | Der Server konnte nicht auf den Palworld Player Manager zugreifen. |

## Beispiele

### List all known players

```http
GET /v1/pdapi/players
```

### Refresh an admin player selector

```http
GET /v1/pdapi/players
```

## Szenarien

- Build a dropdown of online and known players.
- Find the correct `UserId` or `PlayerUID` before calling reward, punishment, or inventory endpoints.
- Audit who is online before sending a message or scheduled maintenance warning.

## Related

- [GET /player](player.md) for one player.
- [POST /kick](kick.md), [POST /ban](ban.md), and reward endpoints use the same player identifier style.
