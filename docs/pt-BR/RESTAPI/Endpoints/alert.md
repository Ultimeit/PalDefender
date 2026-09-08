# POST /Alert



**Ponto final:** `POST /v1/pdapi/Alert`

**Autenticação:** Token do portador

**Permissão:** `REST.Messages.Alert`

## Objetivo

Envia uma mensagem de alerta ao servidor.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com `Message` string.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/alert.md"

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
| `400` | `BROADCAST_ALERT_FAILED` | O servidor não conseguiu enviar a mensagem de alerta. |

## Exemplos

### Enviar alerta de reinicialização

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Restart now."
}
```

### Enviar alerta multilinha

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Server restart in 5 minutes.\nPlease return to base."
}
```

## Cenários

- Envie avisos de servidor de alta prioridade.
- Use após uma transmissão quando os jogadores precisarem de um aviso final urgente.
- Mantenha os alertas curtos para que possam ser lidos no jogo.
