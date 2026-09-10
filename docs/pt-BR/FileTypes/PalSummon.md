# 📄 `PalSummon.json`

Um arquivo PalSummon define um encontro de local fixo iniciado com `/summon <filename>`. Armazene arquivos em `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/` e PalTemplates referenciados em `Pals/Templates/`.

!!! tip "Pesquisa de ID"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) para `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) para passivos e [paldeck.cc/skills](https://paldeck.cc/skills) para IDs de habilidade usados pelo modelo referenciado.

## Chaves de encontro

| Chave | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `PalTemplate` | string | Obrigatório | Nome de arquivo de um modelo em `Pals/Templates/`; `.json` pode ser omitido. |
| `BossBattleName` | string | ID do Pal | Nome de exibição usado em anúncios, registros, webhooks e resultados de danos. |
| `Uncapturable` | bool | `false` | Impede que o Pal invocado seja capturado. |
| `CapturableAtHealthPercent` | número | `15` | Se capturável, permite a captura apenas nesta porcentagem de HP ou inferior (`0`–`100`). Ignorado quando `Uncapturable` é `true`. |
| `DisableAI` | bool | `false` | Desativa a IA normal. Algum comportamento passivo, como esquiva, ainda pode ocorrer. |
| `DisableDamageMeter` | bool | `false` | Desativa o rastreamento, a caixa de diálogo de resultados e as recompensas de classificação. A recompensa `Default` é concedida a todos os jogadores online. |
| `SpawnScale` | número | `1.0` | Visual/physical multiplicador de tamanho; valores não positivos voltam para `1.0`. |
| `DamageTakenMultiplier` | número | `1.0` | Multiplicador por dano recebido; valores negativos voltam para `1.0`. |
| `DamageDealtMultiplier` | número | `1.0` | Multiplicador por dano causado; valores negativos voltam para `1.0`. |
| `X`, `Y`, `Z` | número | Obrigatório | Coordenadas do mapa. Use `/getpos` para obtê-los. |
| `DisableStatuses` | array | Vazio | Nomes de status a serem suprimidos. Nomes inválidos são ignorados. |
| `Rewards` | object ou array | Vazio | [Definições de recompensa específicas por classificação e padrão](#damage-meter-and-rewards) opcionais. O formato object é recomendado. |

`CapturableAt`, `CapturableAtPercent` e `capturable_at` são aliases de compatibilidade aceitos. `AdditionalEnemyReceiveDamageRate` e `AdditionalEnemyInflictDamageRate` também são aceitos, mas os nomes na tabela são preferidos.

!!! warning "Migração da vida máxima"
    A vida máxima do Pal invocado agora é obtida de `HP` no PalTemplate referenciado. `HealthMultiplier`, `HPMultiplier` e `AdditionalEnemyMaxHPRate` não são mais compatíveis; remova esses campos dos arquivos PalSummon existentes.

## Medidor de danos e recompensas { #damage-meter-and-rewards }

As recompensas são resolvidas depois que o Pal convocado morre ou é capturado. A tabela de classificação de danos é classificada do maior para o menor dano. A caixa de diálogo de resultados mostra os cinco primeiros, destaca os três primeiros e também mostra a posição do jogador receptor quando esse jogador está fora dos cinco primeiros.

Com o rastreamento de danos ativado, cada jogador participante é tratado da seguinte forma:

1. PalDefender procura uma chave numérica `Rewards` que corresponda à classificação final desse jogador.
2. Se essa classificação exata não existir, PalDefender usará `Rewards.Default`.
3. Se nenhum deles existir, esse jogador não receberá recompensa.
4. A recompensa selecionada é rolada separadamente para esse jogador. Dois jogadores que usam a mesma definição de `Default` podem, portanto, receber resultados aleatórios diferentes.

Somente os participantes que ainda estiverem online e tiverem um controlador de jogador disponível quando o encontro terminar poderão receber recompensas classificadas. Uma recompensa numerada não inclui a recompensa `Default`; ele o substitui por essa classificação.

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

Neste exemplo, o primeiro colocado recebe ambos os drops garantidos, o segundo colocado recebe uma quantidade aleatória de EXP e todos os outros participantes classificados independentemente têm 75% de chance de receber 1.000 dinheiro.

As chaves de classificação devem ser números inteiros positivos escritos como chaves JSON object, como `"1"`, `"2"` ou `"10"`. `"0"`, classificações negativas e nomes arbitrários são inválidos. `Default` é correspondido sem distinção entre maiúsculas e minúsculas.

??? note "Formulário Array"
    `Rewards` também pode ser um array. Array o elemento 0 é a classificação 1, o elemento 1 é a classificação 2 e assim por diante. O formulário array não pode definir `Default`, portanto o formulário object é mais claro e recomendado.

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### Estrutura de definição de recompensa

Cada classificação e `Default` contém uma definição de recompensa. Uma definição pode conter ambos:

- `Drops`: entradas avaliadas direta e independentemente.
- `Pools`: grupos que controlam como as entradas são selecionadas.

Também pode conter as abreviações de progressão `EXP`, `TechnologyPoints` e `AncientTechnologyPoints`. As abreviações são garantidas e úteis quando não precisam de sua própria configuração `Chance`, `Weight` ou `Unique`.

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### Tipos de entrada de recompensa

Cada inscrição deve definir exatamente um tipo de recompensa. Não combine um item, ovo e campo de progressão na mesma entrada.

| Recompensa | Campos obrigatórios | Campos opcionais | Notas |
| --- | --- | --- | --- |
| Artigo | `ItemID` | `Count`, `Chance`, `Weight`, `Unique` | `Count` é padronizado como `1`. |
| Ovo Pal | `EggID`, `PalTemplate` | `Count`, `Level`, `Chance`, `Weight`, `Unique` | `Count` é padronizado como `1`; `Level: 0` usa o nível do modelo. |
| Experiência | `EXP` | `Chance`, `Weight`, `Unique` | O valor `EXP` é o valor ou intervalo. |
| Pontos de tecnologia | `TechnologyPoints` | `Chance`, `Weight`, `Unique` | O valor do campo é o valor ou intervalo. |
| Pontos de tecnologia antiga | `AncientTechnologyPoints` | `Chance`, `Weight`, `Unique` | O valor do campo é o valor ou intervalo. |

`Chance`, `Weight` e `Unique` só são eficazes nos contextos descritos abaixo. Um campo aceito pelo analisador não significa que ele afeta todos os modos de distribuição.

Os nomes de campos canônicos acima são recomendados. O analisador também aceita estes aliases:

| Campo canônico | Aliases aceitos |
| --- | --- |
| `ItemID` | `ItemId`, `ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`, `Num` |
| `EXP` | `Exp`, `Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### Valores fixos, intervalos e chances

Os valores podem ser um número inteiro fixo ou um intervalo inclusivo:

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- Os valores de `Count`, EXP e pontos de tecnologia devem ser números inteiros de pelo menos `1`.
- Um intervalo precisa de `Min` e `Max`, e `Max` não deve ser inferior a `Min`.
- Intervalos de texto como `"1-3"` são inválidos; use `{ "Min": 1, "Max": 3 }`.
- Ovo `Level` pode ser `0`; isso mantém o nível do PalTemplate referenciado. Um nível positivo substitui o nível do modelo e é limitado ao nível 255 quando o ovo é concedido.
- `Chance` aceita um número ou texto numérico com um `%` opcional, por exemplo `30`, `30.5` ou `"30%"`.
- `Chance: 0` nunca é bem-sucedido, `Chance: 100` sempre é bem-sucedido e os valores devem ficar entre `0` e `100`.
- Para uma chance estritamente entre 0 e 100, o lançamento gerado deve ser inferior ao valor configurado. Uma rolagem de exatamente `30.0`, portanto, falha em `Chance` de `30`.

### Quedas diretas

Cada entrada em `Drops` é avaliada de forma independente. Não há relacionamento de escolha entre entradas vizinhas. Faltando `Chance` significa `100`.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

O dinheiro está garantido. Cada um dos pontos de munição, EXP e tecnologia faz sua própria jogada de chance. Zero, um, dois ou todos os três lançamentos opcionais podem ser bem-sucedidos.

`Weight` e `Unique` não funcionam em `Drops` direto e produzem avisos. Use `Chance` para quedas diretas opcionais.

## Conjuntos de saques

Um pool primeiro lança seu próprio `Chance`. Se o pool falhar, nenhuma de suas entradas será considerada. Se for bem-sucedido, `Mode` decide como as entradas serão avaliadas.

| Chave da piscina | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `Name` | string | Vazio | Etiqueta de diagnóstico opcional. Isso não afeta a seleção. |
| `Mode` | string | `OneOf` | `OneOf`, `Pick`, `All` ou `Independent`. A correspondência não diferencia maiúsculas de minúsculas. |
| `Chance` | texto de número ou porcentagem | `100` | Chance de que todo o pool seja ativado. |
| `Rolls` | número inteiro | `1` | Número de seleções em `Pick`; ignorado pelos outros modos. |
| `Unique` | bool | `true` | Política de repetição padrão para `Pick`; uma entrada pode substituí-la. |
| `Entries` | array | Obrigatório | Lista não vazia de entradas de recompensa. |

`One` é aceito como alias para `OneOf` e `PickN` como alias para `Pick`, mas os nomes dos modos canônicos são recomendados.

| Modo | Quantas entradas podem ser concedidas? | Usa `Weight`? | Usa a entrada `Chance`? | Usa `Rolls` / `Unique`? |
| --- | --- | --- | --- | --- |
| `OneOf` | Exatamente um se o pool for bem-sucedido | Sim | Não | Não |
| `Pick` | Até `Rolls` seleções | Sim | Não | Sim |
| `All` | Cada entrada uma vez se o pool for bem-sucedido | Não | Não | Não |
| `Independent` | Zero em todas as entradas | Não | Sim | Não |

Todos os quatro modos ainda usam o `Chance` no nível do pool. Vários pools em uma definição de recompensa são processados ​​de forma independente e seus resultados são adicionados ao `Drops` direto.

### `OneOf`: um resultado ponderado

`OneOf` é o modo padrão. Se a chance no nível do pool for bem-sucedida, exatamente uma entrada será selecionada. A probabilidade de uma entrada é seu `Weight` dividido pela soma de todos os pesos de entrada.

```json
{
    "Pools": [
        {
            "Name": "Equipment jackpot",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

Os pesos totalizam 20. Dependendo do sucesso do pool, as quatro entradas têm probabilidades de 35%, 35%, 25% e 5%. Como o pool em si é ativado apenas 35% das vezes, a chance absoluta do ovo é `35% × 5% = 1.75%`.

- `Weight` ausente é padronizado como `1`.
- `Weight` deve ser um número inteiro de pelo menos `1`; remova uma entrada em vez de atribuir peso `0`.
- `Rolls` é ignorado e produz um aviso porque `OneOf` sempre seleciona uma vez.
- O `Chance` de nível básico é ignorado e produz um aviso. Use `Weight` para controlar a probabilidade de seleção relativa.
- `Unique` não tem efeito prático porque apenas uma entrada está selecionada.

### `Pick`: vários resultados ponderados sem repetições

`Pick` repete a seleção ponderada `Rolls` vezes. Com o `Unique: true` padrão, uma entrada selecionada é removida antes da próxima seleção e não pode ser selecionada novamente. Os pesos são recalculados a partir das entradas restantes após cada seleção.

```json
{
    "Pools": [
        {
            "Name": "Choose two different rewards",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

Isso concede duas entradas diferentes. Se `Rolls` for maior que o número de entradas exclusivas disponíveis, a seleção será interrompida quando não houver mais entradas; não é um erro.

### `Pick`: permitindo resultados repetidos

Defina `Unique` do pool como `false` para manter as entradas selecionadas disponíveis para lançamentos posteriores. Concessões repetidas do mesmo item são mescladas antes da entrega.

```json
{
    "Pools": [
        {
            "Name": "Three supply rolls",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

Todos os três lançamentos podem selecionar Dinheiro, todos podem selecionar munição ou os resultados podem ser mistos. Por exemplo, selecionar Dinheiro duas vezes produz uma concessão de dinheiro de 10.000, em vez de duas concessões separadas.

### `Pick`: substituindo `Unique` por entrada

Um `Unique` de nível de entrada substitui o padrão do pool apenas para essa entrada. Isso permite recompensas comuns repetíveis e recompensas de jackpot único no mesmo pool.

```json
{
    "Pools": [
        {
            "Name": "Repeatable currency with unique jackpots",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

O dinheiro permanece na lista de candidatos após ser selecionado porque sua entrada diz `Unique: false`. A armadura e o capacete herdam `Unique: true` do conjunto e são removidos após a seleção. O inverso também é válido: um pool pode usar `Unique: false` enquanto uma entrada específica usa `Unique: true`.

### `All`: conceder todas as entradas

`All` concede cada entrada exatamente uma vez quando o `Chance` no nível do pool é bem-sucedido.

```json
{
    "Pools": [
        {
            "Name": "Complete reward bundle",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`Weight`, `Chance` de nível básico e `Unique` não afetam `All`. `Rolls` é ignorado e produz um aviso. Para tornar todo o pacote opcional, defina o `Chance` do pool; para tornar as entradas individuais opcionais, use `Independent` ou `Drops` direto.

### `Independent`: role cada entrada separadamente

`Independent` verifica cada entrada e usa o próprio `Chance` de cada entrada. Ele não pode conceder nenhuma entrada, uma entrada, várias entradas ou todas as entradas.

```json
{
    "Pools": [
        {
            "Name": "Independent bonus rolls",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

Primeiro, o pool tem 80% de chance de ser ativado. Se for ativado, o Money é garantido porque sua entrada omite `Chance`; as outras três entradas acumulam 50%, 10% e 5% de forma independente.

- A entrada ausente `Chance` é padronizada como `100`.
- `Weight` e `Unique` não afetam este modo.
- `Rolls` é ignorado e produz um aviso porque cada entrada é verificada uma vez.

### Combinando quedas diretas e vários pools

Use vários pools quando um destinatário precisar receber várias camadas de recompensa estruturadas de forma independente.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "One equipment item",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "Two supply rolls",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "Rare independent bonuses",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

O Dinheiro direto e EXP sempre se aplicam. O primeiro conjunto adiciona um item de equipamento, o segundo faz duas seleções ponderadas de suprimentos com reposição e o terceiro faz duas jogadas de bônus independentes. Um jogador pode receber resultados de todos os grupos porque os grupos não competem entre si.

### Recompensas de ovos de Pal

Um ovo precisa de `EggID` e `PalTemplate`. O modelo é carregado de `Pals/Templates/` e `.json` pode ser omitido. `Count` controla quantos ovos são concedidos. `Level: 0` ou um nível omitido mantém o nível do modelo; um valor ou intervalo fixo positivo o substitui.

```json
{
    "Pools": [
        {
            "Name": "One random egg reward",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

Se um modelo de ovo não puder ser importado quando a recompensa for concedida, PalDefender registrará um erro e ignorará a recompensa do ovo.

### Mesclando resultados repetidos

Os resultados de quedas diretas e todos os pools são combinados antes da entrega:

- Itens com o mesmo `ItemID` são mesclados adicionando suas contagens.
- Os ovos se fundem apenas quando `EggID`, `PalTemplate` e o `Level` rolado são todos idênticos.
- EXP, pontos de tecnologia e pontos de tecnologia antiga são somados.
- Os totais concedíveis de itens e pontos de tecnologia são limitados ao máximo assinado de 32 bits (`2,147,483,647`).

Isso significa que resultados repetidos de `Pick` não criam linhas de inventário duplicadas na solicitação de recompensa. Ovos com diferentes níveis rolados permanecem como recompensas separadas.

### Distribuição de `DisableDamageMeter`

Quando `DisableDamageMeter` é `true`, PalDefender não cria uma tabela de classificação de danos e não usa recompensas de classificação numérica. Em vez disso, ele rola `Rewards.Default` separadamente para **cada jogador que estiver online quando o encontro terminar**, incluindo jogadores que não causaram dano ao Pal invocado.

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

O dinheiro é concedido a todos os jogadores online. Cada jogador lança independentemente as duas recompensas de pontos opcionais. Se `Default` estiver ausente ou vazio, ninguém receberá uma recompensa neste modo e PalDefender gravará um aviso no log.

### Combinações inválidas e ignoradas

Dados de recompensa inválidos impedem o carregamento do arquivo PalSummon. Campos desconhecidos ou ignorados contextualmente produzem avisos para que erros ortográficos e configurações ineficazes fiquem visíveis no log PalDefender.

| Configuração | Resultado |
| --- | --- |
| Uma entrada contém `ItemID` e `EXP` | Erro: uma entrada pode definir apenas um tipo de recompensa. |
| Uma entrada de recompensa não possui item, ovo ou campo de progressão | Erro: PalDefender não sabe o que conceder. |
| `Count: 0`, `Weight: 0` ou `Rolls: 0` | Erro: esses valores devem ser pelo menos `1`. |
| Um intervalo omite `Min` ou `Max` ou tem `Max < Min` | Erro. |
| `Chance` está fora de `0`–`100` | Erro. |
| Um pool não tem `Entries`, um `Entries` array vazio ou um valor diferente de array | Erro. |
| `Chance` é colocado em uma entrada `OneOf`, `Pick` ou `All` | Aviso; a chance de entrada é ignorada. |
| `Rolls` está definido em `OneOf`, `All` ou `Independent` | Aviso; `Rolls` é ignorado. |
| `Weight` ou `Unique` é colocado diretamente em `Drops` | Aviso; use `Chance` para quedas diretas. |
| Um campo desconhecido como `Wieght` está presente | Aviso; o campo não é utilizado. |

Use JSON válido sem comentários ou vírgulas finais. Revise os avisos de carregamento mesmo quando a invocação ainda estiver carregando: os avisos geralmente identificam uma configuração que não tem efeito.

## Exemplo completo

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Arena Anubis",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "Winner bonus",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## Lista de verificação de validação

1. Teste primeiro o modelo referenciado com `/givemepal_j <template>`.
2. Use `/getpos` para `X`, `Y` e `Z`; RCON deve fornecer um UserId para `/getpos`.
3. Use JSON válido sem comentários ou vírgulas finais.
4. Use apenas um tipo de recompensa por entrada de recompensa.
5. Verifique se cada pool tem um `Entries` array não vazio e usa apenas campos que afetam seu `Mode` selecionado.
6. Execute `/summon <filename>` e verifique o log PalDefender para erros e avisos de validação precisos.
