# POST /ban/{player_identifier}



**Ponto final:** `POST /v1/pdapi/ban/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Punishments.Ban`

## Objetivo

Bane um usuário e registra o banimento em `Banlist.json`. O alvo pode ser chutado se estiver online.

## Parâmetros de caminho

- `player_identifier`: `UserId`, `PlayerUID` ou outro identificador de player compatível.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Campos opcionais JSON: `Reason` string e `IP` booleano. Defina `IP` como `true` somente quando você também quiser banir o endereço IP resolvido.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/ban.md"

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
| `400` | `IP_UNAVAILABLE` | `IP` era `true`, mas o servidor não conseguiu resolver um IP para o usuário de destino. |

## Exemplos

### Banir um usuário Steam

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Chargeback fraud"
}
```

### Banir um usuário PS5 e seu IP resolvido

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Ban evasion",
    "IP": true
}
```

## Cenários

- Banir um jogador por `UserId` após análise de moderação.
- Inclua um motivo claro para que os futuros funcionários possam entender a entrada na lista banida.
- Use [GET /banlist](banlist.md) para verificar o registro ativo. Os dados relacionados ao banimento não são mais gerenciados em `Config.json`.
