# GET /guild/{guild_id}



**Endpunkt:** `GET /v1/pdapi/guild/<guild_id>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Guild.Read`

## Zweck

Gibt eine Gilde mit detaillierten Mitglieder- und Basis-/Campdaten zurück.

## Pfadparameter

- `guild_id`: Gildenkennung, üblicherweise aus [GET /guilds](guilds.md) kopiert.

## Query-Parameter

Keine.

## Request-Body

Kein Request-Body.

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` | Keine Gilde entsprach der angegebenen `guild_id`. |

## Beispiele

### Gildenmitglieder und Basislager lesen

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### Eine andere Gilde anhand ihrer GUID lesen

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Szenarien

- Vor dem Löschen einer Basis deren Eigentümer prüfen.
- Für Supportanfragen Gildenmitglieder und Basislagerdaten prüfen.
- Nutze Camp-IDs aus der Antwort vorsichtig mit [POST /deletebase](deletebase.md).
