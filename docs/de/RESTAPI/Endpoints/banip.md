# POST /banip/{ip}



**Endpunkt:** `POST /v1/pdapi/banip/<ip>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Punishments.BanIP`

## Zweck

Bannt eine IP-Adresse und speichert sie in `Banlist.json`.

## Pfadparameter

- `ip`: IP address to ban.

## Query-Parameter

Keine.

## Request-Body

Optionale JSON-Felder: `Reason` als String und `UserId` als String, wenn der IP-Bann einem Benutzer zugeordnet werden soll.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/banip.md"

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
| `400` | `VALIDATION_FAILED` | Ein optionales Anfragefeld besitzt den falschen JSON-Typ. |

## Beispiele

### Nur eine IP sperren

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Bot traffic"
}
```

### Eine IP sperren und einen GDK-Benutzer zuordnen

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Alt account abuse",
    "UserId": "gdk_2533274898765432"
}
```

## Szenarien

- Wiederholten Missbrauch von derselben IP nach Prüfung durch das Team unterbinden.
- Wenn bekannt, `UserId` zuordnen, damit die Sperrliste leichter geprüft werden kann.
- Nutze [GET /banlist](banlist.md) mit `ip`, um den aktiven Eintrag zu prüfen.
