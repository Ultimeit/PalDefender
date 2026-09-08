# 📄 `PalTemplate.json`

use <https://paldeck.cc/creator> para criar esses arquivos com muito mais facilidade!

!!! tip "Pesquisa de ID"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) para `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) para `Passives` e [paldeck.cc/skills](https://paldeck.cc/skills) para `ActiveSkills` e `LearntSkills`.

| Chave | Tipo | Descrição                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID` | string | ID interno do Pal a ser gerado. Pesquise valores [`PalID`](https://paldeck.cc/pals) válidos no Paldeck. |
| `UniqueNPCID` | string | ID interno do Pal para gerar NPCs.                                               |
| `Nickname` | string | Apelido opcional dado ao Pal.                                                 |
| `SkinId` | string | Substituição de skin para o Pal (usado para aparências personalizadas). Use cmd `/getskinids` para recuperar IDs. |
| `Gender` | string | `"Male"`, `"Female"` ou `"None"`.                                                   |
| `Level` | interno | O nível do Pal.                                                               |
| `Exp` | interno | Pontos de experiência.                                                                  |
| `Shiny` | bool | Se o Pal é brilhante.                                                           |
| `PartnerSkillLevel` | interno | Nível da habilidade do parceiro do Pal. Não pode ser inferior a 1!                           |
| `CondensedPals` | interno | Número de Pals merged/condensed neste.                                      |
| `UnusedStatusPoints` | interno | Pontos de status disponíveis para distribuição manual. Provavelmente usado apenas para jogadores?    |
| `FriendshipPoints` | interno | Valor de amizade para o Pal.                                               |
| `PhysicalHealth` | string | Estado de saúde física. Os nomes válidos incluem `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick` | string | Estado de doença do trabalhador. Os nomes válidos incluem `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter` | bool | Marca o Pal como um personagem importado.                                    |
| `HP` / `SP` / `MP` | número | Valores básicos de saúde, resistência e mana.                                              |
| `Shield` | número | Valor do escudo.                                                              |
| `Hunger` / `MaxHunger` | interno | Valores atuais e máximos de fome.                                                      |
| `SAN` | interno | Sanidade (estabilidade mental do Pal).                                               |
| `Support` | interno | Nível de suporte (usado para comportamento e habilidades de IA).                                    |
| `CraftSpeed` | interno | Multiplicador de velocidade de criação.                                                          |
| `PalSouls` | object | Bônus de alma passivos. Contém: `Health`, `Attack`, `Defense`, `CraftSpeed`. Os valores normais recomendados são controlados pelas suas regras de importação. |
| `IVs` | object | Valores estatísticos individuais. Contém: `Health`, `AttackMelee`, `AttackShot`, `Defense`. Os valores normais recomendados são controlados pelas suas regras de importação. |
| `ActiveSkills` | array | Lista de habilidades equipadas. PalDefender 1.9.0 não trunca PalTemplates administrativos em três entradas; cada entrada permanece equipada. Pesquise [IDs de habilidades](https://paldeck.cc/skills) válidos no Paldeck. O comportamento normal do game/UI ainda pode assumir a contagem de slots padrão. |
| `LearntSkills` | array | Habilidades que o Pal aprendeu e pode usar. Evite colocar habilidades ativas aqui. Pesquise [IDs de habilidade](https://paldeck.cc/skills) válidos no Paldeck. |
| `Passives` | array | Traços passivos que o Pal possui. Pals normais devem usar até 4 passivas. Pesquise valores [`PassiveID`](https://paldeck.cc/passives) válidos no Paldeck. |
| `ExtraWorkSuitabilities` | object | Tipos e níveis de trabalho aprimorados (por exemplo, `"Mining": 2`). Tipos de trabalho disponíveis: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`.  |
| `DisableWorkPreferences` | array | Tipos de trabalho que o Pal se recusa a fazer. Tipos de trabalho disponíveis: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Conjunto de instruções

1. Crie um arquivo JSON por Pal personalizado em `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Use um nome de arquivo exclusivo, por exemplo `RaidRewardAnubis.json`. Os comandos geralmente podem usar `RaidRewardAnubis` ou `RaidRewardAnubis.json`.
3. Sempre inclua `PalID`. Todo o resto é opcional, mas os valores ausentes usam os padrões PalDefender ou Palworld.
4. Mantenha `Level` em `1` ou superior e `PartnerSkillLevel` em `1` ou superior.
5. Put ataques equipados em `ActiveSkills` e outros ataques conhecidos em `LearntSkills`. PalDefender não move mais entradas ativas extras para habilidades aprendidas.
6. Use IDs exatos para Pals, habilidades, passivos, skins e tipos de trabalho. IDs errados podem não ser importados ou podem ser ignorados.
7. Valide JSON antes de fazer upload. JSON não permite comentários ou vírgulas finais.
8. Se um modelo for importado, mas os valores forem alterados ou bloqueados, verifique o `Pals/ImportRules/Default.json` do servidor e quaisquer arquivos de substituição por Pal.

## Passo a passo de configuração

1. Decida para que serve o modelo: uma simples recompensa de administrador, um chefe de evento, um Pal de teste ou um modelo de spawn para uma convocação.
2. Escolha o `PalID` em [paldeck.cc/pals](https://paldeck.cc/pals). O nome de exibição nem sempre é o ID do arquivo, então copie o ID exatamente.
3. Adicione apenas os campos que deseja controlar. Um modelo curto é mais fácil de depurar do que um modelo muito grande.
4. Escolha habilidades de [paldeck.cc/skills](https://paldeck.cc/skills). Put ataques equipados em `ActiveSkills`; adicione outros ataques conhecidos a `LearntSkills`.
5. Escolha passivos de [paldeck.cc/passives](https://paldeck.cc/passives). Para uso normal, mantenha até quatro passivos, a menos que seu servidor permita mais intencionalmente.
6. Salve o arquivo em `Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
7. Teste primeiro com `/givemepal_j <filename>`. Depois disso, use o mesmo modelo para `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, REST API ou `PalSummon.json`.

## Exemplos de explicações

O exemplo mínimo abaixo cria um Anúbis nível 50 com três ataques equipados e dois passivos. É adequado para teste porque possui apenas o `PalID` obrigatório mais alguns campos comuns.

O exemplo maior é intencionalmente extremo. Ele mostra a estrutura disponível para almas, IVs, habilidades, passivas e substituições de adequação ao trabalho. Em servidores que usam regras de importação, valores altos podem ser limitados ou bloqueados.

## Exemplo mínimo

```json
{
    "PalID": "Anubis",
    "Nickname": "Arena Anubis",
    "Gender": "None",
    "Level": 50,
    "PartnerSkillLevel": 1,
    "HP": 3500,
    "SAN": 100,
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "RockLance"
    ],
    "Passives": [
        "Legend",
        "CraftSpeed_up3"
    ]
}
```

## Exemplo

Este arquivo deve ser armazenado em: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate` pode ser qualquer nome exclusivo nessa pasta. Este será o argumento de comando para `/givepal_j` e `/spawnpal_j`!)

```json
{
    "PalID": "Anubis",
    "Nickname": "OPnubis",
    "Gender": "None",
    "Level": 255,
    "Shiny": true,
    "PartnerSkillLevel": 255,
    "HP": 999999,
    "SP": 999999,
    "MP": 999999,
    "Hunger": 999999,
    "MaxHunger": 999999,
    "SAN": 999999,
    "Support": 999999,
    "CraftSpeed": 999999,
    "PalSouls": {
        "Health": 255,
        "Attack": 255,
        "Defense": 255,
        "CraftSpeed": 255
    },
    "IVs": {
        "Health": 255,
        "AttackMelee": 255,
        "AttackShot": 255,
        "Defense": 255
    },
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "Unique_Anubis_LowRoundKick"
    ],
    "Passives": [
        "Legend",
        "PAL_ALLAttack_up3",
        "Deffence_up3",
        "Vampire",
        "Stamina_Up_3",
        "EternalFlame",
        "PAL_Sanity_Down_3",
        "Invader",
        "SwimSpeed_up_3",
        "Rare",
        "Nushi",
        "PAL_FullStomach_Down_3",
        "CraftSpeed_up3",
        "Salvation",
        "Witch",
        "MoveSpeed_up_3",
        "SwimSpeed_up_2",
        "CraftSpeed_up2",
        "Deffence_up2",
        "ElementBoost_Normal_2_PAL",
        "PAL_FullStomach_Down_2",
        "ElementBoost_Dragon_2_PAL",
        "ElementBoost_Earth_2_PAL",
        "PAL_ALLAttack_up2",
        "ElementBoost_Fire_2_PAL",
        "ElementBoost_Ice_2_PAL",
        "Stamina_Up_1",
        "TrainerLogging_up1",
        "ElementBoost_Thunder_2_PAL",
        "ElementBoost_Aqua_2_PAL",
        "ElementBoost_Dark_2_PAL",
        "TrainerMining_up1",
        "TrainerWorkSpeed_UP_1",
        "SalePrice_Up_1",
        "Test_PalEgg_HatchingSpeed_Up",
        "MoveSpeed_up_2",
        "CoolTimeReduction_Up_1",
        "ElementBoost_Leaf_2_PAL",
        "TrainerDEF_UP_1",
        "TrainerATK_UP_1",
        "PAL_Sanity_Down_2",
        "ElementResist_Normal_1_PAL",
        "ElementBoost_Dragon_1_PAL",
        "ElementResist_Leaf_1_PAL",
        "PAL_ALLAttack_up1",
        "ElementBoost_Thunder_1_PAL",
        "ElementResist_Dark_1_PAL",
        "ElementBoost_Ice_1_PAL",
        "PAL_FullStomach_Down_1",
        "ElementResist_Dragon_1_PAL",
        "ElementResist_Earth_1_PAL",
        "SalePrice_Up_2",
        "Stamina_Up_2",
        "ElementBoost_Leaf_1_PAL",
        "Deffence_up1",
        "ElementResist_Ice_1_PAL",
        "ElementBoost_Aqua_1_PAL",
        "CoolTimeReduction_Up_2",
        "ElementResist_Thunder_1_PAL",
        "MoveSpeed_up_1",
        "Alien",
        "PAL_Sanity_Down_1",
        "ElementBoost_Earth_1_PAL",
        "ElementBoost_Fire_1_PAL",
        "CraftSpeed_up1",
        "SwimSpeed_up_1",
        "ElementResist_Fire_1_PAL",
        "ElementBoost_Dark_1_PAL",
        "ElementResist_Aqua_1_PAL",
        "ElementBoost_Normal_1_PAL"
    ],
    "ExtraWorkSuitabilities": {
        "EmitFlame": 5,
        "Watering": 5,
        "Seeding": 5,
        "GenerateElectricity": 5,
        "Handcraft": 5,
        "Collection": 5,
        "Deforest": 5,
        "Mining": 5,
        "OilExtraction": 5,
        "ProductMedicine": 5,
        "Cool": 5,
        "Transport": 5,
        "MonsterFarm": 5,
        "Anyone": 5
    }
}
```
