# GET /guilds



**Ponto final:** `GET /v1/pdapi/guilds`

**Autenticação:** Token do portador

**Permissão:** `REST.Guilds.Read`

## Objetivo

Lista guildas conhecidas com informações resumidas. Use este endpoint para descobrir IDs de guilda antes de solicitar uma guilda específica.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/guilds.md"

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

## Exemplos

### Listar todas as guildas

```http
GET /v1/pdapi/guilds
```

### Atualizar dados do painel da guilda

```http
GET /v1/pdapi/guilds
```

## Cenários

- Crie um seletor de guilda em um painel de administração.
- Encontre o `guild_id` para [GET /guild](guild.md).
- Visão geral das contagens da base de auditoria, contagens de membros e propriedade da guilda.
