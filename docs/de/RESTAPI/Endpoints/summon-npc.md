# POST /summon/npc

**Endpunkt:** `POST /v1/pdapi/summon/npc`  
**Authentifizierung:** Bearer-Token  
**Berechtigung:** `REST.Summon.NPC`

## Zweck

Spawnt einen NPC an festen Kartenkoordinaten.

## Request-Body

| Feld | Typ | Erforderlich | Beschreibung |
| --- | --- | --- | --- |
| `NPCID` | string | Ja | NPC-ID oder NPC-Character-ID. |
| `X`, `Y`, `Z` | number | Ja | Kartenkoordinaten. |
| `Level` | integer | Nein | NPC-Level (Standard `1`). |
| `Uncapturable` | bool | Nein | Verhindert das Fangen (Standard `false`). |
| `DisableAI` | bool | Nein | Deaktiviert die normale KI (Standard `false`). |

## Antwortschema

--8<-- "_snippets/de/restapi/schemas/summon-npc.md"

## Fehler

Zusätzlich zu den üblichen Authentifizierungs-/Request-Fehlern kann diese Route `VALIDATION_FAILED` oder `SUMMON_NPC_FAILED` zurückgeben.

## Beispiel

```http
POST /v1/pdapi/summon/npc
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "NPCID": "PIDF_Soldier_AssaultRifle",
    "Level": 30,
    "X": 230,
    "Y": -486,
    "Z": 4097
}
```
