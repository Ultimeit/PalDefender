# POST /give/paltemplate/{player_identifier}



**Ponto final:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**Autenticação:** Token do portador

**Permissão:** `REST.PalTemplates.Give`

## Objetivo

Fornece um ou mais Pals de arquivos em `Pals/Templates/`.

## Parâmetros de caminho

- `player_identifier`: `UserId` ou `PlayerUID` para o jogador alvo.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

JSON object com `PalTemplates`, um array de nomes de arquivos de modelo. A extensão `.json` pode ser incluída para maior clareza.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | O corpo não contém um `PalTemplates` array. |
| `400` | `VALIDATION_FAILED` | Um ou mais nomes de arquivo de modelo são inválidos, não podem ser importados ou não cabem no armazenamento Pal. |

## Exemplos

### Dê um modelo de Pal para um jogador Steam

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### Dê modelos de recompensa de ataque a um jogador PS5

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## Cenários

- Use quando as recompensas precisarem de habilidades específicas, passivas, IVs, almas, apelidos ou valores de adequação ao trabalho.
- Use [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md) para criar o modelo primeiro.
- As regras de importação em `Pals/ImportRules/` podem bloquear ou ajustar modelos antes de serem concedidos.
