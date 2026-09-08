# POST /give/paleggs/{player_identifier}



**Ponto final:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.PalEggs.Give`

## Objetivo

Dá um ou mais ovos de Pal ao jogador alvo.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com `PalEggs`, um array de concessões de ovos. `EggID` é um [`ItemID`](https://paldeck.cc/items). Cada ovo deve usar [`PalID`](https://paldeck.cc/pals) ou `PalTemplate`, não ambos.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | O corpo não contém um `PalEggs` array. |
| `400` | `VALIDATION_FAILED` | Uma ou mais concessões de ovos são inválidas, não podem ser importadas ou não cabem no inventário. |

## Exemplos

### Dê um ovo nivelado a um jogador Steam

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### Fornece ovo apoiado por modelo por PlayerUID

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## Cenários

- Dê ovos de evento sem gerar o Pal imediatamente.
- Use `PalID` para ovos simples e `PalTemplate` para conteúdos de ovos personalizados.
- A solicitação poderá falhar se o ovo [`ItemID`](https://paldeck.cc/items) for inválido ou se o inventário do jogador não tiver espaço.
