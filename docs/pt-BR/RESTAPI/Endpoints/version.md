# GET /version



**Ponto final:** `GET /v1/pdapi/version`

**Autenticação:** Token do portador

**Permissão:** `REST.Version.Read`

## Objetivo

Use esse endpoint como verificação de integridade e versão de ferramentas, painéis e scripts.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/version.md"

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

## Exemplos

### Verificação de integridade e versão

```http
GET /v1/pdapi/version
```

## Cenários

- Use-o após configurar o token REST API para confirmar o funcionamento da autenticação.
- Use-o antes de chamar endpoints se sua ferramenta precisar de uma versão mínima de PalDefender.
- Use-o para monitoramento, pois é a menor solicitação somente leitura.
