# GET /pals/{player_identifier}



**Ponto final:** `GET /v1/pdapi/pals/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Pals.Read`

## Objetivo

Lista os Pals do jogador alvo. Os identificadores Pal nas respostas podem ser pesquisados ​​em [paldeck.cc/pals](https://paldeck.cc/pals).

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/pals.md"

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
| `404` | `PLAYER_NOT_FOUND` | Nenhum jogador online correspondeu ao `player_identifier` fornecido. |
| `404` | `PLAYER_STATE_NOT_FOUND` | O player existe, mas seu `APalPlayerState` não estava disponível. |

## Exemplos

### Leia Pals para um jogador PS5

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### Leia Pals por PlayerUID

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## Cenários

- Revise um jogador antes das ações de suporte.
- Confirme se um Pal recompensa chegou após usar [POST /give/pals](give-pals.md) ou [POST /give/paltemplate](give-paltemplate.md).
- Investigue relatos sobre Pals desaparecidos ou inesperados.
