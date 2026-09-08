# POST /SendPlayerMessage



**Ponto final:** `POST /v1/pdapi/SendPlayerMessage`

**Autenticação:** Token do portador

**Permissão:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## Objetivo

Envia uma mensagem para um ou mais jogadores alvo.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com `SendType`, `Message` e `UserID` ou `UserIDs`. Os valores comuns de `SendType` incluem `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant` e `PlayerLogVeryImportant`.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` | O corpo da solicitação está vazio. |
| `400` | `INVALID_JSON` | O corpo da solicitação não é válido JSON. |
| `400` | `VALIDATION_FAILED` | `SendType`, `Message`, `UserID`, or `UserIDs` is missing, empty, duplicated, or has the wrong type. |
| `400` | `PLAYER_NOT_FOUND` | Não foi possível encontrar um ou mais IDs de usuário ou UIDs de jogadores de destino. |
| `400` | `SEND_MESSAGE_FAILED` | A validação foi aprovada, mas o servidor rejeitou a operação de envio de mensagem. |
| `400` | `REQUEST_FAILED` | O retorno de chamada do thread do jogo gerou uma exceção. |
| `500` | `REQUEST_TIMEOUT` | O retorno de chamada do thread de jogo interno não foi concluído em 5 segundos. |

## Exemplos

### Enviar bate-papo do jogador para um usuário

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived."
}
```

### Envie logs importantes para destinos mistos

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "The event starts in 10 minutes."
}
```

## Cenários

- Envie avisos de reinicialização direta aos jogadores selecionados.
- Envie respostas de suporte de um painel de administração.
- Use `UserID` para um destino e `UserIDs` para vários destinos, não ambos.
