# POST /learntech/{player_identifier}



**Ponto final:** `POST /v1/pdapi/learntech/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Techs.Learn`

## Objetivo

Aprende uma, muitas ou todas as tecnologias para um jogador.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

`Technology` pode ser um único [`TechID`](https://paldeck.cc/technology), a string `"All"` ou um array de strings [`TechID`](https://paldeck.cc/technology). Não coloque `"All"` dentro de um array.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` está faltando ou não é um string/array no formato esperado. |
| `400` | `VALIDATION_FAILED` | O `Technology` array contém um identificador de tecnologia não string, `All` ou um identificador de tecnologia inválido. |

## Exemplos

### Aprenda uma tecnologia para um player Steam

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Aprenda diversas tecnologias para um jogador PS5

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Aprenda todas as tecnologias por PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Cenários

- Desbloqueie uma receita que faltava para suporte.
- Desbloqueie todas as tecnologias para contas de teste.
- Valide os IDs de tecnologia em [paldeck.cc/technology](https://paldeck.cc/technology) antes de enviar a solicitação.
