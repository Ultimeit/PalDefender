# POST /give/items/{player_identifier}



**Ponto final:** `POST /v1/pdapi/give/items/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Items.Give`

## Objetivo

Dá um ou mais itens ao jogador alvo.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com `Items`, um array de concessões de itens. Cada entrada precisa de um [`ItemID`](https://paldeck.cc/items) e um `Count` positivo.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` | O corpo não contém um `Items` array. |
| `400` | `VALIDATION_FAILED` | Uma ou mais concessões de itens são inválidas, não são suportadas, são muito grandes ou não cabem no inventário. |
| `500` | `GRANT_FAILED` | A validação foi aprovada, mas o servidor falhou ao adicionar itens ao inventário. |

## Exemplos

### Dê munição e um lançador para um jogador Steam

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### Dê moeda a um jogador PS5

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## Cenários

- Use para pacotes de compensação após uma reversão.
- Use para integrações de lojas onde um serviço confiável concede itens comprados.
- Valide o [`ItemID`](https://paldeck.cc/items) primeiro; os nomes de exibição nem sempre são IDs válidos.
