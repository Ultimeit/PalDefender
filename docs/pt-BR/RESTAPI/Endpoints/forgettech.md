# POST /forgettech/{player_identifier}



**Ponto final:** `POST /v1/pdapi/forgettech/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.Techs.Forget`

## Objetivo

Esquece uma, muitas ou todas as tecnologias de um jogador.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

`Technology` pode ser um único [`TechID`](https://paldeck.cc/technology), a string `"All"` ou um array de strings [`TechID`](https://paldeck.cc/technology). Não coloque `"All"` dentro de um array.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/forgettech.md"

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

### Esqueça uma tecnologia para um player GDK

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Esqueça várias tecnologias por PlayerUID

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Esqueça todas as tecnologias para um jogador Steam

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Cenários

- Remova uma tecnologia concedida por engano.
- Redefina uma conta de teste com `"All"`.
- Confirme o estado atual com [GET /techs](techs.md) antes e depois da solicitação.
