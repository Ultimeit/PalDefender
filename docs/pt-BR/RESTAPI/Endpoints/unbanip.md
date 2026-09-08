# POST /unbanip/{ip}



**Ponto final:** `POST /v1/pdapi/unbanip/<ip>`

**Autenticação:** Token do portador

**Permissão:** `REST.Punishments.UnbanIP`

## Objetivo

Desbane um endereço IP em `Banlist.json`.

## Parâmetros de caminho

- `ip`: endereço IP para cancelar o banimento.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Campo opcional JSON: `Reason` string.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/unbanip.md"

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
| `404` | `BAN_NOT_FOUND` | O `ip` fornecido não foi banido ativamente. |

## Exemplos

### Desbanir um IP com razão

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Temporary block expired"
}
```

### Desbanir um IP com motivo padrão

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## Cenários

- Remova um banimento de IP após investigação.
- Use quando um jogador ainda estiver bloqueado após o cancelamento do banimento no nível do usuário porque o registro de IP permanece ativo.
- Use [GET /banlist](banlist.md) com `ip` para verificar o resultado.
