# POST /banip/{ip}



**Ponto final:** `POST /v1/pdapi/banip/<ip>`

**Autenticação:** Token do portador

**Permissão:** `REST.Punishments.BanIP`

## Objetivo

Bane um endereço IP e o registra em `Banlist.json`.

## Parâmetros de caminho

- `ip`: endereço IP a ser banido.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Campos opcionais JSON: `Reason` string e `UserId` string quando o banimento de IP deve ser associado a um usuário.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/banip.md"

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

## Exemplos

### Banir apenas um IP

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Bot traffic"
}
```

### Banir um IP e anexar um usuário GDK

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Alt account abuse",
    "UserId": "gdk_2533274898765432"
}
```

## Cenários

- Pare de abusos repetidos do mesmo IP após revisão da equipe.
- Associe `UserId` quando conhecido para que a lista banida seja mais fácil de auditar.
- Use [GET /banlist](banlist.md) com `ip` para verificar o registro ativo.
