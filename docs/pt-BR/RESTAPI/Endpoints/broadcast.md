# POST /Broadcast



**Ponto final:** `POST /v1/pdapi/Broadcast`

**Autenticação:** Token do portador

**Permissão:** `REST.Messages.Broadcast`

## Objetivo

Transmite uma mensagem de bate-papo para o servidor.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com um `Message` string obrigatório.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/broadcast.md"

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
| `400` | `VALIDATION_FAILED` | `Message` está ausente, vazio ou não é um string. |

## Exemplos

### Transmita um aviso de reinicialização

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

## Cenários

- Anuncie a manutenção programada.
- Envie mensagens automatizadas de início de eventos.
- Use [POST /Alert](alert.md) quando a mensagem deveria ser um alerta em vez de um chat de transmissão normal.
