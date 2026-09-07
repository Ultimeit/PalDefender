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

--8<-- "_snippets/de/restapi/schemas/players.md"

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

### Alle bekannten Spieler auflisten

```http
GET /v1/pdapi/players
```

### Eine Spielerauswahl im Adminbereich aktualisieren

```http
GET /v1/pdapi/players
```

## Szenarien

- Eine Auswahlliste der Online- und bekannten Spieler erstellen.
- Vor dem Aufruf von Belohnungs-, Straf- oder Inventarendpunkten die richtige `UserId` oder `PlayerUID` ermitteln.
- Vor einer Nachricht oder geplanten Wartungswarnung prüfen, wer online ist.

## Related

- [GET /player](player.md) für einen einzelnen Spieler.
- [POST /kick](kick.md), [POST /ban](ban.md) und Belohnungsendpunkte verwenden dieselbe Art von Spielerkennung.
