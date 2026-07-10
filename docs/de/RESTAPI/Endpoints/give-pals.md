# POST /give/pals/{player_identifier}



**Endpunkt:** `POST /v1/pdapi/give/pals/<player_identifier>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Pals.Give`

## Zweck

Gibt einen oder mehrere Pals anhand von ID und Level.

## Pfadparameter

- `player_identifier`: `UserId` oder `PlayerUID` des Zielspielers.

## Query-Parameter

Keine.

## Request-Body

JSON-Objekt mit `Pals`, einem Array von Pal-Vergaben. Jeder Eintrag benötigt eine [`PalID`](https://paldeck.cc/pals) und ein positives `Level`.

## Antwortschema

--8<-- "_snippets/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` | Der Body enthält kein `Pals`-Array. |
| `400` | `VALIDATION_FAILED` | One or more Pal grants are invalid, or the player has insufficient Pal storage space. |

## Beispiele

### Starter-Pal an einen GDK-Spieler geben

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### Event-Pals per PlayerUID geben

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## Szenarien

- Einfache Pal-Belohnungen vergeben, ohne eine Template-Datei zu pflegen.
- Für zufällige Belohnungsskripte nutzen, die nur `PalID` und `Level` variieren.
- Die Anfrage kann fehlschlagen, wenn der Spieler nicht gefunden wird, die [`PalID`](https://paldeck.cc/pals) ungültig ist oder nicht genug Pal-Speicherplatz vorhanden ist.
