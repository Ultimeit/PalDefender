# GET /items/{player_identifier}



**Ponto final:** `GET /v1/pdapi/items/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Items.Read`

## Objetivo

Lista os itens do jogador alvo. Os identificadores de itens nas respostas podem ser pesquisados ​​em [paldeck.cc/items](https://paldeck.cc/items).

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` | O jogador alvo, o estado do jogador, os dados de inventário ou o contêiner de inventário comum não puderam ser resolvidos. |
| `500` | `REQUEST_TIMEOUT` | O retorno de chamada do thread de jogo interno não foi concluído em 5 segundos. |

## Exemplos

### Leia o inventário de um jogador Steam

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### Leia o inventário de um jogador GDK

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## Cenários

- Verifique o estoque antes de dar compensação.
- Confirme um [`ItemID`](https://paldeck.cc/items) antes de usar [POST /give/items](give-items.md).
- Solucione relatórios de problemas sobre itens ausentes.
