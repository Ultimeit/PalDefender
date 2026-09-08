# POST /summon/npc

**Point final :** `POST /v1/pdapi/summon/npc`
**Auth :** Jeton du porteur
**Autorisation :** `REST.Summon.NPC`

## Objectif

Génère un NPC à des coordonnées cartographiques fixes.

## Corps de la demande

| Champ | Type | Obligatoire | Descriptif |
| --- | --- | --- | --- |
| `NPCID` | string | Oui | ID NPC ou ID de caractère NPC. |
| `X`, `Y`, `Z` | numéro | Oui | Coordonnées de la carte. |
| `Level` | integer | Non | Niveau NPC (`1` par défaut). |
| `Uncapturable` | bool | Non | Empêche la capture (par défaut `false`). |
| `DisableAI` | bool | Non | Désactive l'IA normale (`false` par défaut). |

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/summon-npc.md"

## Erreurs

Outre les erreurs standard authentication/request, cette route peut renvoyer `VALIDATION_FAILED` ou `SUMMON_NPC_FAILED`.

## Exemple

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
