# POST /summon/npc

**Ponto final:** `POST /v1/pdapi/summon/npc`
**Autenticação:** Token do portador
**Permissão:** `REST.Summon.NPC`

## Objetivo

Gera um NPC em coordenadas fixas do mapa.

## Solicitar corpo

| Campo | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `NPCID` | string | Sim | NPC ID ou NPC ID do caractere. |
| `X`, `Y`, `Z` | número | Sim | Coordenadas do mapa. |
| `Level` | integer | Não | Nível NPC (padrão `1`). |
| `Uncapturable` | bool | Não | Impede a captura (padrão `false`). |
| `DisableAI` | bool | Não | Desativa a IA normal (padrão `false`). |

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/summon-npc.md"

## Erros

Juntamente com os erros authentication/request padrão, esta rota pode retornar `VALIDATION_FAILED` ou `SUMMON_NPC_FAILED`.

## Exemplo

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
