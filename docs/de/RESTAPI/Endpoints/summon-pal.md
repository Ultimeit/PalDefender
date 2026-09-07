# POST /summon/pal

**Endpunkt:** `POST /v1/pdapi/summon/pal`  
**Authentifizierung:** Bearer-Token  
**Berechtigung:** `REST.Summon.Pal`

## Zweck

Spawnt einen Pal an festen Kartenkoordinaten. Die Anfrage muss genau eines von `PalID` oder `PalTemplate` enthalten.

## Request-Body

| Feld | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `PalID` | string | Eines von beiden | Pal-Art-ID. Schließt `PalTemplate` aus. |
| `PalTemplate` | string | Eines von beiden | Dateiname aus `Pals/Templates/`; verwendet Pal und Level des Templates. |
| `X`, `Y`, `Z` | number | Ja | Kartenkoordinaten. |
| `Level` | integer | Nein | Level bei `PalID`-Summons (Standard `1`). Bei einem Template ignoriert. |
| `Uncapturable` | bool | Nein | Verhindert das Fangen (Standard `false`). |
| `DisableAI` | bool | Nein | Deaktiviert die normale KI (Standard `false`). |
| `DisableDamageMeter` | bool | Nein | Deaktiviert die Schadenserfassung (Standard `false`). |
| `HealthMultiplier` | number | Nein | Positiver Lebensmultiplikator (Standard `1.0`). `HPMultiplier` wird als Alias akzeptiert. |
| `DisableStatuses` | array | Nein | Zu unterdrückende Statusnamen. |

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/summon-pal.md"

## Fehler

Zusätzlich zu den Standardantworten `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED` und `REQUEST_TIMEOUT` kann diese Route `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED` oder `SUMMON_PAL_FAILED` zurückgeben.

## Beispiel

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true,
    "HealthMultiplier": 5.0
}
```
