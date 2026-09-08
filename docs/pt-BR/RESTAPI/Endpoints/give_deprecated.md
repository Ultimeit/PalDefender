# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>Deprecated</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>Deprecated</span> endpoint legado"
    Este endpoint de recompensa legado está obsoleto. Prefira os pontos finais de recompensa dividida: [dar progressão](./give-progression.md), [dar itens](./give-items.md), [dar Pals](./give-pals.md), [dar modelos de Pals](./give-paltemplate.md) e [dar ovos a Pals](./give-paleggs.md).


## Esquema de resposta

--8<-- "_snippets/restapi/schemas/give_deprecated.md"

## Respostas de erro

Este endpoint está obsoleto e pode não estar presente nas compilações atuais. Quando disponíveis, os corpos dos erros usam o mesmo envelope de erro REST que o API atual.

| HTTP | Código de erro | Quando isso acontece |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | O cabeçalho `Authorization` está ausente, malformado ou não corresponde a um token de portador configurado. |
| `403` | `MISSING_PERMISSION` | O token é válido, mas não inclui permissão para esta rota obsoleta. |
| `400` | `INVALID_JSON` | Um corpo de solicitação foi fornecido, mas não pôde ser analisado como JSON. |
| `400` | `REQUEST_FAILED` | A operação de recompensa herdada falhou ao validar ou aplicar a solicitação. |
| `500` | `REQUEST_TIMEOUT` | O retorno de chamada do thread de jogo interno não foi concluído em 5 segundos. |

## Exemplos

### Conceda EXP e itens

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### Grant Pals e ovos

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

??? info "POST `/v1/pdapi/give` — Concede EXP / itens / Pals / ovos (atômico)"
    ## POST `/v1/pdapi/give`
    ### O que isso faz
    Concede recompensas a um jogador alvo em uma única operação semelhante a uma transação no servidor:

    - EXPand/or
    - itens and/or
    - Pals and/or
    - ovos
    dependendo do corpo da solicitação.

    ### Comportamento central
    Este endpoint destina-se a se comportar **atomicamente**:

    - ou tudo é concedido
    - ou nada é concedido

    Se alguma parte falhar (entrada inválida, falta de espaço no inventário, IDs inválidos, etc.), o servidor deverá rejeitar a solicitação e não aplicá-la parcialmente.

    ### Por que isso é importante
    As ferramentas administrativas não devem acidentalmente:

    - dê EXP, mas não itens
    - dê alguns itens, mas falhe em itens posteriores
    - gerar Pals sem colocar itens

    O comportamento atômico evita estados confusos e “tíquetes de suporte infernais”.

    ### O que pode conceder
    Dependendo da sua implementação, a solicitação pode incluir:

    - `EXP` — adiciona experiência
    - `Relics` — adiciona pontos de relíquia codificados por tipo de relíquia
    - `TechnologyPoints` — adiciona pontos técnicos
    - `AncientTechnologyPoints` — adiciona pontos tecnológicos antigos
    - `UnlockTechnology` / `Techs[]` — aprenda tecnologias
    - `Items[]` — forneça um ou mais itens com contagens
    - `Pals[]` — forneça Pals por ID + nível
    - `PalTemplates[]` — importa modelos pal por nome de arquivo
    - `PalEggs[]` — ovos por ID + pal ID/modelo, opcionalmente com nível


    ### Respostas de erro

    Este endpoint está obsoleto e pode não estar presente nas compilações atuais. Quando disponível, espere o mesmo envelope de erro REST usado pelo API atual: `INVALID_TOKEN` (`401`) para falha na autenticação do portador e `MISSING_PERMISSION` (`403`) quando o token é autenticado, mas não tem permissão para chamar a rota. As falhas de validação de solicitação são retornadas como objetos de erro JSON; migre para os endpoints de recompensa dividida para obter códigos de erro específicos do endpoint.

    ### Exemplos

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### Validação e casos de falha comuns
    Razões típicas pelas quais os administradores acertam erros:

    - Espaço de estoque: espaço insuficiente para todos os itens → falha em toda a solicitação
    - IDs inválidos: `ItemID`, `PalID`, `EggID` desconhecidos ou arquivo de modelo ausente → falha
    - Valores inválidos:
        - contagens negativas/zero (dependendo das regras)
        - níveis inválidos (muito low/high ou não numéricos)
        - campos obrigatórios ausentes (por exemplo, nenhum `UserID`)
    - Player não encontrado/não carregado:
        - ID do usuário desconhecido
        - jogador que não está online no momento (dependendo de como seu servidor lida com concessões offline)

    ### Devoluções
    Contagem de erros e mensagens de erro. Se o status não for 200, verifique `Errors` quantos erros ocorreram. `Error` contém a lista detalhada do que falhou.
