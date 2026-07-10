# POST /ban/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/ban/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Punishments.Ban`

## Zweck

Bannt einen Benutzer und speichert den Bann in `Banlist.json`. Das Ziel kann gekickt werden, wenn es aktuell online ist.

## Pfadparameter

- `player_identifier`: `UserId`, `PlayerUID`, or another supported player identifier.

## Query-Parameter

Keine.

## Request-Body

Optionale JSON-Felder: `Reason` als String und `IP` als Boolean. Setze `IP` nur dann auf `true`, wenn auch die aufgelöste IP-Adresse gebannt werden soll.

## Antwortschema

--8<-- "_snippets/restapi/schemas/ban.md"

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
| `400` | `VALIDATION_FAILED` | An optional request field has the wrong JSON type. |
| `400` | `IP_UNAVAILABLE` | `IP` was `true`, but the server could not resolve an IP for the target user. |

## Beispiele

### Ban a Steam user

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Chargeback fraud"
}
```

### Ban a PS5 user and their resolved IP

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Ban evasion",
    "IP": true
}
```

## Szenarien

- Ban a player by `UserId` after moderation review.
- Include a clear reason so future staff can understand the banlist entry.
- Nutze [GET /banlist](banlist.md), um den aktiven Eintrag zu prüfen. Bannbezogene Daten werden nicht mehr in `Config.json` verwaltet.
