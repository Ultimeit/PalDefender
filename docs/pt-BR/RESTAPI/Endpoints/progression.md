# GET /progression/{player_identifier}



**Ponto final:** `GET /v1/pdapi/progression/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Progression.Read`

## Objetivo

Lê valores de progressão do jogador, como EXP, estado relacionado ao nível, totais de relíquias e totais de pontos de tecnologia.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` | O jogador alvo, conta, dados de personagens individuais, dados de registro ou dados de tecnologia não puderam ser resolvidos. |
| `500` | `REQUEST_TIMEOUT` | O retorno de chamada do thread de jogo interno não foi concluído em 5 segundos. |

## Exemplos

### Leia a progressão por UserID do PS5

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### Leia a progressão por PlayerUID

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Cenários

- Confirme os valores atuais antes de conceder a progressão.
- Verifique uma ação de suporte após [POST /give/progression](give-progression.md).
- Crie um painel de visão geral do jogador em um painel de administração confiável.
