# POST /deletebase/{base_camp_id}



**Endpunkt:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**Auth:** Bearer-Token

**Berechtigung:** `REST.Base.Delete`

## Zweck

Löscht eine Basis/ein Camp anhand der Base-Camp-ID. Das ist eine destruktive Admin-Aktion.

## Pfadparameter

- `base_camp_id`: Base camp identifier, usually copied from guild/base data.

## Query-Parameter

Keine.

## Request-Body

Optionales leeres JSON-Objekt. Bestätige die ID, bevor du die Anfrage sendest.

## Antwortschema

--8<-- "_snippets/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | The `base_camp_id` path value is not a valid GUID. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | Der Server konnte nicht auf `UPalBaseCampManager` zugreifen. |
| `404` | `BASE_CAMP_NOT_FOUND` | No base camp matched the supplied GUID. |
| `500` | `DELETE_BASE_FAILED` | Das Base Camp wurde gefunden, aber Zerstoerung/Bereinigung ist fehlgeschlagen. |

## Beispiele

### Delete a base camp by GUID

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### Delete another base camp by GUID

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## Szenarien

- Remove abandoned or broken bases after staff review.
- Nutze [GET /guilds](guilds.md) und [GET /guild](guild.md), um vor dem Löschen das richtige Camp zu identifizieren.
- Do not use this endpoint for routine cleanup unless your staff process already verifies ownership and backups.
