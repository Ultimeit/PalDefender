# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>Veraltet</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>Veraltet</span> alter Endpunkt"
    Dieser alte Belohnungsendpunkt ist veraltet. Nutze bevorzugt die getrennten Endpunkte: [Fortschritt vergeben](./give-progression.md), [Gegenstände vergeben](./give-items.md), [Pals vergeben](./give-pals.md), [Pal-Templates vergeben](./give-paltemplate.md) und [Pal-Eier vergeben](./give-paleggs.md).


## Antwortschema

--8<-- "_snippets/de/restapi/schemas/give_deprecated.md"

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

### EXP und Gegenstände vergeben

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

### Pals und Eier vergeben

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

??? info "POST `/v1/pdapi/give` — EXP / Gegenstände / Pals / Eier atomar vergeben"
    ## POST `/v1/pdapi/give`
    ### Funktionsweise
    Vergibt Belohnungen in einem einzigen transaktionsähnlichen serverseitigen Vorgang an einen Zielspieler:

    - EXP und/oder
    - Gegenstände und/oder
    - Pals und/oder
    - Eier,
    abhängig vom Anfrageinhalt.

    ### Kernverhalten
    Dieser Endpunkt soll **atomar** arbeiten:

    - Entweder wird alles vergeben,
    - oder es wird nichts vergeben.

    Wenn ein Teil fehlschlägt (ungültige Eingabe, fehlender Inventarplatz, ungültige IDs usw.), sollte der Server die Anfrage ablehnen und sie nicht teilweise anwenden.

    ### Warum das wichtig ist
    Administrationswerkzeuge dürfen nicht versehentlich:

    - EXP, aber keine Gegenstände vergeben,
    - einige Gegenstände vergeben und bei späteren scheitern,
    - Pals erzeugen, ohne Gegenstände abzulegen.

    Atomares Verhalten verhindert inkonsistente Zustände und aufwendige Supportfälle.

    ### Mögliche Vergaben
    Je nach Implementierung kann die Anfrage Folgendes enthalten:

    - `EXP` — fügt Erfahrung hinzu
    - `Relics` — fügt nach Relikttyp indizierte Reliktpunkte hinzu
    - `TechnologyPoints` — fügt Technologiepunkte hinzu
    - `AncientTechnologyPoints` — fügt antike Technologiepunkte hinzu
    - `UnlockTechnology` / `Techs[]` — erlernt Technologien
    - `Items[]` — vergibt einen oder mehrere Gegenstände mit Mengen
    - `Pals[]` — vergibt Pals anhand von ID und Stufe
    - `PalTemplates[]` — importiert Pal-Templates anhand des Dateinamens
    - `PalEggs[]` — vergibt Eier anhand von Ei-ID und Pal-ID oder Template, optional mit Stufe


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

    ### Validierung und häufige Fehlerfälle
    Typische Gründe für Fehler:

    - Inventarplatz: Nicht genug Platz für alle Gegenstände → gesamte Anfrage schlägt fehl
    - Ungültige IDs: unbekannte `ItemID`, `PalID`, `EggID` oder fehlende Template-Datei → Anfrage schlägt fehl
    - Ungültige Werte:
        - negative oder Nullmengen (abhängig von den Regeln)
        - ungültige Stufen (zu niedrig/hoch oder nicht numerisch)
        - fehlende Pflichtfelder (z. B. keine `UserID`)
    - Spieler nicht gefunden oder nicht geladen:
        - Benutzer-ID nicht bekannt
        - Spieler derzeit nicht online (abhängig von der Behandlung von Offline-Vergaben)

    ### Rückgabe
    Fehleranzahl und Fehlermeldungen. Wenn `status` nicht 200 ist, prüfe `Errors`, um zu sehen, wie viele Fehler aufgetreten sind. `Error` enthält die detaillierte Liste der fehlgeschlagenen Teile.
