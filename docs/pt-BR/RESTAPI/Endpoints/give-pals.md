# POST /give/pals/{player_identifier}



**Ponto final:** `POST /v1/pdapi/give/pals/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Pals.Give`

## Objetivo

Dá um ou mais Pals por ID e nível.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com `Pals`, um array de concessões Pal. Cada entrada precisa de um [`PalID`](https://paldeck.cc/pals) e um `Level` positivo.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` | O corpo não contém um `Pals` array. |
| `400` | `VALIDATION_FAILED` | Uma ou mais concessões de Pal são inválidas ou o jogador não tem espaço de armazenamento de Pal suficiente. |

## Exemplos

### Dê um Pal inicial para um jogador GDK

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### Dê Pals ao evento por PlayerUID

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## Cenários

- Dê recompensas simples ao Pal sem manter um arquivo de modelo.
- Use para scripts de recompensa aleatórios que variam apenas `PalID` e `Level`.
- A solicitação pode falhar se o player não puder ser encontrado, se o [`PalID`](https://paldeck.cc/pals) for inválido ou se não houver espaço de armazenamento suficiente no Pal.
