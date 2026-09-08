# POST /unban/{user_id}



**Ponto final:** `POST /v1/pdapi/unban/<user_id>`

**Autenticação:** Token do portador

**Permissão:** `REST.Punishments.Unban`

## Objetivo

Cancela o banimento de um ID de usuário em `Banlist.json`.

## Parâmetros de caminho

- `user_id`: ID do usuário para cancelar o banimento.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Campo opcional JSON: `Reason` string.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/unban.md"

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
| `400` | `VALIDATION_FAILED` | Um campo de solicitação opcional tem o tipo JSON errado. |
| `404` | `BAN_NOT_FOUND` | O `user_id` fornecido não foi banido ativamente. |

## Exemplos

### Desbanir um usuário Steam

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### Desbanir um usuário PS5 com motivo padrão

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## Cenários

- Remova o banimento de um usuário após a aprovação da apelação.
- Mantenha um motivo para a trilha de auditoria.
- Use [GET /banlist](banlist.md) com `userId` ou `q` para verificar o resultado.
