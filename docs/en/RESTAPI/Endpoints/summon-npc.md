# POST /summon/npc

**Endpoint:** `POST /v1/pdapi/summon/npc`  
**Auth:** Bearer token  
**Permission:** `REST.Summon.NPC`

## Purpose

Spawns an NPC at fixed map coordinates.

## Request body

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `NPCID` | string | Yes | NPC ID or NPC character ID. |
| `X`, `Y`, `Z` | number | Yes | Map coordinates. |
| `Level` | integer | No | NPC level (default `1`). |
| `Uncapturable` | bool | No | Prevents capture (default `false`). |
| `DisableAI` | bool | No | Disables normal AI (default `false`). |

## Response schema

--8<-- "_snippets/restapi/schemas/summon-npc.md"

## Errors

Alongside standard authentication/request errors, this route may return `VALIDATION_FAILED` or `SUMMON_NPC_FAILED`.

## Example

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
