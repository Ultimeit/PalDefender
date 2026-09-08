# POST /kick/{player_identifier}



**Ponto final:** `POST /v1/pdapi/kick/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Punishments.Kick`

## Objetivo

Expulsa um jogador online sem criar um registro de banimento.

## Parâmetros de caminho

- `player_identifier`: `UserId`, `PlayerUID` ou outro identificador de player compatível.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Campo opcional JSON: `Reason` string.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` | O jogador alvo não está online ou não foi encontrado. |

## Exemplos

### Chute um jogador GDK com razão

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "AFK in event area"
}
```

### Expulsar um jogador Steam com motivo padrão

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## Cenários

- Remova um jogador antes da manutenção.
- Chute um jogador preso para que ele possa se reconectar.
- Use [POST /ban](ban.md) quando o jogador não puder voltar.
