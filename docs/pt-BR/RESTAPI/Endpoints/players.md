# GET /players



**Ponto final:** `GET /v1/pdapi/players`

**Autenticação:** Token do portador

**Permissão:** `REST.Players.Read`

## Objetivo

Lista jogadores conhecidos com informações de identificação e status. Use-o para criar seletores de jogadores para ferramentas administrativas.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | O servidor não conseguiu acessar o gerenciador de jogadores Palworld. |

## Exemplos

### Liste todos os jogadores conhecidos

```http
GET /v1/pdapi/players
```

### Atualizar um seletor de player administrativo

```http
GET /v1/pdapi/players
```

## Cenários

- Crie uma lista suspensa de jogadores online e conhecidos.
- Encontre o `UserId` ou `PlayerUID` correto antes de chamar os pontos finais de recompensa, punição ou inventário.
- Audite quem está online antes de enviar uma mensagem ou aviso de manutenção programada.

## Relacionado

- [GET /player](player.md) para um jogador.
- [POST /kick](kick.md), [POST /ban](ban.md) e pontos finais de recompensa usam o mesmo estilo de identificador de jogador.
