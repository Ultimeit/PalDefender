# POST /summon/pal

**Ponto final:** `POST /v1/pdapi/summon/pal`
**Autenticação:** Token do portador
**Permissão:** `REST.Summon.Pal`

## Objetivo

Gera um Pal em coordenadas fixas do mapa. A solicitação deve fornecer exatamente um entre `PalID` ou `PalTemplate`.

## Solicitar corpo

| Campo | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `PalID` | string | Um dos | ID da espécie Pal. Mutuamente exclusivo com `PalTemplate`. |
| `PalTemplate` | string | Um dos | Nome do arquivo de `Pals/Templates/`; usa o Pal e o nível do modelo. |
| `X`, `Y`, `Z` | número | Sim | Coordenadas do mapa. |
| `Level` | integer | Não | Nível para convocação `PalID` (padrão `1`). Ignorado para um modelo. |
| `Uncapturable` | bool | Não | Impede a captura (padrão `false`). |
| `DisableAI` | bool | Não | Desativa a IA normal (padrão `false`). |
| `DisableDamageMeter` | bool | Não | Desativa o rastreamento de danos (padrão `false`). |
| `HealthMultiplier` | número | Não | Multiplicador de integridade positivo (padrão `1.0`). `HPMultiplier` é aceito como alias. |
| `DisableStatuses` | array | Não | Nomes de status a serem suprimidos. |

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/summon-pal.md"

## Erros

Juntamente com as respostas padrão `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED` e `REQUEST_TIMEOUT`, esta rota pode retornar `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED` ou `SUMMON_PAL_FAILED`.

## Exemplo

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
