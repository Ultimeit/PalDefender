# GET /techs/{player_identifier}



**Ponto final:** `GET /v1/pdapi/techs/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Techs.Read`

## Objetivo

Lista informações de tecnologia para um jogador. Os identificadores de tecnologia podem ser pesquisados ​​em [paldeck.cc/technology](https://paldeck.cc/technology).

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | O jogador alvo, a conta do jogador, os dados tecnológicos ou a tabela tecnológica não puderam ser resolvidos. |
| `500` | `REQUEST_TIMEOUT` | O retorno de chamada do thread de jogo interno não foi concluído em 5 segundos. |

## Exemplos

### Leia tecnologias desbloqueadas por UserID

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### Leia as tecnologias desbloqueadas por PlayerUID

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## Cenários

- Verifique se um jogador já possui um [`TechID`](https://paldeck.cc/technology) antes de aprendê-lo ou esquecê-lo.
- Crie uma página de administração que separe as tecnologias desbloqueadas das disponíveis.
- Progressão da auditoria após ações de apoio.
