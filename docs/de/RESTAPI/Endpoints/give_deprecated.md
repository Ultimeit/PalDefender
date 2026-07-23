# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>Veraltet</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>Veraltet</span> legacy endpoint"
    Dieser alte Belohnungs-Endpunkt ist veraltet. Nutze bevorzugt die getrennten Belohnungs-Endpunkte: [give progression](./give-progression.md), [give items](./give-items.md), [give pals](./give-pals.md), [give pal templates](./give-paltemplate.md) und [give Pal eggs](./give-paleggs.md).


## Antwortschema

--8<-- "_snippets/restapi/schemas/give_deprecated.md"

## Fehlerantworten

Dieser Endpunkt ist veraltet und in aktuellen Builds möglicherweise nicht vorhanden. Falls er verfügbar ist, nutzen Fehlerantworten dasselbe REST-Fehlerformat wie die aktuelle API.

| HTTP | Fehlercode | Wann es passiert |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | Der `Authorization`-Header fehlt, ist fehlerhaft oder passt zu keinem konfigurierten Bearer-Token. |
| `403` | `MISSING_PERMISSION` | Das Token ist gültig, enthält aber keine Berechtigung für diese veraltete Route. |
| `400` | `INVALID_JSON` | Ein Request-Body wurde gesendet, konnte aber nicht als JSON gelesen werden. |
| `400` | `REQUEST_FAILED` | Die alte Belohnungsoperation ist beim Validieren oder Anwenden der Anfrage fehlgeschlagen. |
| `500` | `REQUEST_TIMEOUT` | Der interne Game-Thread-Callback wurde nicht innerhalb von 5 Sekunden abgeschlossen. |

## Beispiele

### Grant EXP and items

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### Grant Pals and eggs

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

## POST `/v1/pdapi/give` — Grant EXP / items / pals / eggs (atomic) { .toc-only }
??? info "POST `/v1/pdapi/give` — Grant EXP / items / pals / eggs (atomic)"
    ## POST `/v1/pdapi/give`
    ### What it does
    Grants rewards to a target player in a single server-side transaction-like operation:

    - EXP and/or
    - items and/or
    - pals and/or
    - eggs
    depending on the request body.

    ### Core behavior
    Dieser Endpunkt soll **atomar** arbeiten:

    - either everything is granted
    - or nothing is granted

    Wenn ein Teil fehlschlägt (ungültige Eingabe, fehlender Inventarplatz, ungültige IDs usw.), sollte der Server die Anfrage ablehnen und sie nicht teilweise anwenden.

    ### Why this matters
    Admin tooling must not accidentally:

    - give EXP but not items
    - give some items but fail on later items
    - spawn pals without placing items

    Atomic behavior avoids messy states and “support tickets from hell”.

    ### What it can grant
    Depending on your implementation, the request may include:

    - `EXP` — adds experience
    - `Relics` — adds relic points keyed by relic type
    - `TechnologyPoints` — adds tech points
    - `AncientTechnologyPoints` — adds ancient tech points
    - `UnlockTechnology` / `Techs[]` — learn technologies
    - `Items[]` — give one or more items with counts
    - `Pals[]` — give pals by ID + level
    - `PalTemplates[]` — import pal templates by filename
    - `PalEggs[]` — eggs by ID + pal ID / template, optionally with level


    ### Fehlerantworten

    Dieser Endpunkt ist veraltet und in aktuellen Builds möglicherweise nicht vorhanden. Falls er verfügbar ist, nutzt er dasselbe REST-Fehlerformat wie die aktuelle API: `INVALID_TOKEN` (`401`) bei fehlgeschlagener Bearer-Authentifizierung und `MISSING_PERMISSION` (`403`), wenn das Token authentifiziert ist, die Route aber nicht aufrufen darf. Validierungsfehler werden als JSON-Fehlerobjekte zurückgegeben; migriere für spezifische Fehlercodes auf die getrennten Belohnungs-Endpunkte.

    ### Beispiele

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### Validation & common failure cases
    Typische Gründe für Fehler:

    - Inventory space: not enough room for all items → fail the entire request
    - Invalid IDs: unknown `ItemID`, `PalID`, `EggID`, or missing template file → fail
    - Invalid values:
        - negative / zero counts (depending on rules)
        - invalid levels (too low/high, or non-numeric)
        - missing required fields (e.g., no `UserID`)
    - Player not found / not loaded:
        - user ID not known
        - player not currently online (depending on how your server handles offline grants)

    ### Rueckgabe
    Fehleranzahl und Fehlermeldungen. Wenn `status` nicht 200 ist, prüfe `Errors`, um zu sehen, wie viele Fehler aufgetreten sind. `Error` enthält die detaillierte Liste der fehlgeschlagenen Teile.
