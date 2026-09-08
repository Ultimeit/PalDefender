# GET /guild/{guild_id}



**Ponto final:** `GET /v1/pdapi/guild/<guild_id>`

**Autenticação:** Token do portador

**Permissão:** `REST.Guild.Read`

## Objetivo

Retorna uma guilda com informações detalhadas sobre membros e base/camp.

## Parâmetros de caminho

- `guild_id`: Identificador da guilda, geralmente copiado de [GET /guilds](guilds.md).

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` | Nenhuma guilda correspondeu ao `guild_id` fornecido. |

## Exemplos

### Leia a lista de guildas e acampamentos

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### Leia outra guilda por GUID

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Cenários

- Investigue a propriedade da base antes de excluí-la.
- Revise os membros da guilda e os dados do acampamento para solicitações de suporte.
- Use cuidadosamente os IDs de acampamento da resposta com [POST /deletebase](deletebase.md).
