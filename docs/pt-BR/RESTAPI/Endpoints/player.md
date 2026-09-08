# GET /player/{player_identifier}



**Ponto final:** `GET /v1/pdapi/player/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Player.Read`

## Objetivo

Retorna um jogador. O identificador pode ser um identificador de jogador compatível, como `UserId` ou `PlayerUID`.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Nenhum corpo de solicitação.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/player.md"

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
| `404` | `PLAYER_NOT_FOUND` | Nenhum jogador online correspondeu ao `player_identifier` fornecido. |
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | O jogador foi encontrado, mas não foi possível carregar os dados da conta do jogador. |

## Exemplos

### Pesquisa por ID de usuário Steam

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### Pesquisa por PlayerUID

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## Cenários

- Abra uma página de detalhes do jogador após selecionar uma linha de `GET /players`.
- Confirme a meta antes de dar recompensas ou aplicar punições.
- Verifique se o jogador pode atualmente ser resolvido pelo servidor.
