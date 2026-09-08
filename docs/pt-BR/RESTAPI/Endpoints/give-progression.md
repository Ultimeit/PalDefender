# POST /give/progression/{player_identifier}



**Ponto final:** `POST /v1/pdapi/give/progression/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Progression.Give`

## Objetivo

Concede valores de progressão a um jogador.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com pelo menos uma concessão suportada: integer `EXP` positivo, integer `TechnologyPoints` positivo, integer `AncientTechnologyPoints` positivo ou `Relics` como um object não vazio codificado por tipo de relíquia com integer positivo quantidades.


Tipos de relíquias suportadas: `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/give-progression.md"

## Respostas de erro

Os corpos de erro usam esta forma:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP | Código de erro | Quando isso acontece |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | O cabeçalho `Authorization` está ausente, malformado ou não corresponde a um token de portador configurado. |
| `403` | `MISSING_PERMISSION` | O token é válido, mas não inclui essa permissão de endpoint. |
| `400` | `INVALID_JSON` | Um corpo de solicitação foi fornecido, mas não pôde ser analisado como JSON. |
| `400` | `REQUEST_FAILED` | O retorno de chamada do thread do jogo gerou uma exceção ou um resolvedor player/resource compartilhado falhou. |
| `500` | `REQUEST_TIMEOUT` | O retorno de chamada do thread de jogo interno não foi concluído em 5 segundos. |
| `400` | `INVALID_REQUEST` | O corpo não inclui `EXP`, `Relics`, `TechnologyPoints` ou `AncientTechnologyPoints`. |
| `400` | `VALIDATION_FAILED` | Um valor de progressão fornecido está faltando, não integer, não positivo ou internos de progressão obrigatórios estão indisponíveis. |

## Exemplos

### Dê EXP para um jogador GDK

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### Dê pontos e relíquias por PlayerUID

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## Cenários

- Compense os jogadores após uma reversão do salvamento.
- Adicione pontos de tecnologia sem desbloquear uma tecnologia específica.
- Use [POST /learntech](learntech.md) quando quiser desbloquear um [`TechID`](https://paldeck.cc/technology) específico.
