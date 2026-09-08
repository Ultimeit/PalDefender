# GET /banlist



**Ponto final:** `GET /v1/pdapi/banlist`

**Autenticação:** Token do portador

**Permissão:** `REST.Banlist.Read`

## Objetivo

Lê registros de banimentos da lista de banimentos. Os dados relacionados ao banimento são armazenados em `Banlist.json`, não em `Config.json`.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

- `active`: `true`, `false` ou `1` para filtrar o estado ativo.
- `entryType`: Filtrar por tipo de entrada de banimento.
- `userId`: Filtre por ID do usuário.
- `ip` ou `userIP`: Filtre por endereço IP.
- `issuerType`, `issuerName`, `issuerIP`: Filtre por metadados do emissor.
- `reason`: Filtrar por texto de motivo.
- `q`: Pesquisa geral de texto.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/banlist.md"

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

### Listar todos os registros de banimento

```http
GET /v1/pdapi/banlist
```

### Encontre registros ativos de um usuário Steam

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### Pesquisar registros por IP

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## Cenários

- Verifique se um jogador ou IP está banido no momento.
- Pesquise por motivo ou emissor antes de cancelar o banimento.
- Crie um painel de moderação que leia de `Banlist.json` até API.

## Relacionado

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md) e [POST /unbanip](unbanip.md).
