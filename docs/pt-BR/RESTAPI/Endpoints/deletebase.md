# POST /deletebase/{base_camp_id}



**Ponto final:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**Autenticação:** Token do portador

**Permissão:** `REST.Base.Delete`

## Objetivo

Exclui um base/camp pelo ID do acampamento base. Esta é uma ação administrativa destrutiva.

## Parâmetros de caminho

- `base_camp_id`: identificador do acampamento base, geralmente copiado dos dados guild/base.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Opcional vazio JSON object. Confirme o ID antes de enviar a solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | O valor do caminho `base_camp_id` não é um GUID válido. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | O servidor não conseguiu acessar `UPalBaseCampManager`. |
| `404` | `BASE_CAMP_NOT_FOUND` | Nenhum acampamento base correspondeu ao GUID fornecido. |
| `500` | `DELETE_BASE_FAILED` | O acampamento base foi encontrado, mas destruction/cleanup falhou. |

## Exemplos

### Delete um acampamento base por GUID

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### Delete outro acampamento base por GUID

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## Cenários

- Remova bases abandonadas ou quebradas após revisão da equipe.
- Use [GET /guilds](guilds.md) e [GET /guild](guild.md) para identificar o acampamento correto antes da exclusão.
- Não use esse endpoint para limpeza de rotina, a menos que seu processo de equipe já verifique a propriedade e os backups.
