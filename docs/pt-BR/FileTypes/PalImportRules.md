# 📄 `Pals/ImportRules/*.json`


As regras de importação Pal controlam quais arquivos `PalTemplate.json` são permitidos, bloqueados ou ajustados quando importados por comandos ou ações API.

!!! tip "Pesquisa de ID"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) para `AllowedPalIDs`, `BannedPalIDs` e nomes de arquivos de regras por Pal. Use [paldeck.cc/passives](https://paldeck.cc/passives) para `DisallowedPassives`.

## Locais de arquivos

| Arquivo | Objetivo |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | Regras globais de importação para todos os modelos Pal. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | Substituição opcional por Pal. Pesquise [`PalID`](https://paldeck.cc/pals) no Paldeck e use esse ID exato como nome do arquivo. Exemplo: `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | Arquivo de exemplo gerado para referência. Não é uma regra Pal real até que seja copiada e renomeada. |

## Chaves

| Chave | Tipo | Descrição |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | Somente `Default.json`. `AllowAllExceptBanned` permite todos os Pal, exceto `BannedPalIDs`. `AllowOnlyListed` permite apenas `AllowedPalIDs`. |
| `AllowedPalIDs` | array | Somente `Default.json`. Valores [`PalID`](https://paldeck.cc/pals) permitidos quando `PalSelectionMode` é `AllowOnlyListed`. |
| `BannedPalIDs` | array | Somente `Default.json`. [`PalID`](https://paldeck.cc/pals) valores que são sempre negados. |
| `MaxValueLimitAction` | string | `BlockImport` nega modelos acima dos limites configurados. `ClampToMaxValues` reduz os valores aos limites configurados. |
| `DisallowedPassivesAction` | string | `BlockImport` nega modelos com passivos listados. `RemoveFromPal` remove os passivos listados antes da importação. |
| `DisallowedPassives` | array | Valores [`PassiveID`](https://paldeck.cc/passives) afetados por `DisallowedPassivesAction`. |
| `ConditionMode` | string | `None` aplica a regra normalmente. `RequirePalCaptureCount` permite a importação de um Pal somente depois que o jogador tiver capturado Pals suficientes da mesma espécie. |
| `RequiredCaptureCount` | interno | Contagem de capturas da mesma espécie obrigatória quando `ConditionMode` é `RequirePalCaptureCount` (padrão `5`). |
| `Disabled` | bool | Se `true`, desativa as verificações de importação para o conjunto de regras correspondente. |
| `BanIfPalIsImpossible` | bool | Se `true`, PalDefender pode punir importações impossíveis de Pal de acordo com as configurações do servidor. |
| `AllowGenderNone` | bool | Se `false`, os modelos que usam `Gender: "None"` podem ser rejeitados pelas verificações de importação. |
| `MaxLevel` | interno | Nível de Pal mais alto permitido para modelos importados. |
| `MaxRank` | interno | Classificação de habilidade de parceiro mais alta permitida para modelos importados. |
| `PalSouls` | object | Valores máximos permitidos de Pal soul: `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | object | Valores IV máximos permitidos: `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## Conjunto de instruções

1. Comece com `Default.json`. Use-o para políticas em todo o servidor.
2. Use arquivos por Pal apenas quando um Pal precisar de limites diferentes.
3. Os arquivos Per-Pal devem ser nomeados com o Pal ID, por exemplo `Anubis.json`.
4. Não coloque `PalSelectionMode`, `AllowedPalIDs` ou `BannedPalIDs` em arquivos específicos de um Pal. Essas chaves pertencem ao `Default.json`.
5. Use `BlockImport` se desejar moderação estrita.
6. Use `ClampToMaxValues` se preferir aceitar modelos, mas reduzir valores acima do limite.
7. Use `RemoveFromPal` para passivos se preferir a limpeza automática em vez de uma importação com falha.
8. Mantenha os IDs exatos e valide JSON antes de fazer upload.

## Passo a passo de configuração

1. Abra ou crie `Pals/ImportRules/Default.json`.
2. Decida a política global do Pal:
   - Use `AllowAllExceptBanned` quando a maioria dos Pals for permitida e você quiser bloquear apenas alguns.
   - Use `AllowOnlyListed` quando as importações devem ser limitadas a uma lista selecionada.
3. Decida o estilo de moderação:
   - Use `BlockImport` para servidores estritos onde modelos inválidos devem falhar.
   - Use `ClampToMaxValues` quando quiser aceitar modelos, mas reduzir níveis, classificações, almas ou IVs acima do limite.
   - Use `RemoveFromPal` para passivos quando quiser eliminar passivos indesejados em vez de rejeitar o modelo inteiro.
4. Adicione passivos não permitidos de [paldeck.cc/passives](https://paldeck.cc/passives).
5. Adicione Pals banidos ou permitidos de [paldeck.cc/pals](https://paldeck.cc/pals).
6. Adicione uma substituição por Pal somente quando um Pal específico precisar de limites mais rígidos ou mais flexíveis do que o arquivo global.
7. Teste primeiro com um `PalTemplate.json` pequeno antes de importar modelos grandes.

## Configurações comuns

### Permitir a maioria dos Pals, bloquear alguns

Use isto quando recompensas normais de administrador forem permitidas, mas certos Pals não devem ser importados.

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "BannedPalIDs": [
        "JetDragon",
        "BOSS_Anubis"
    ],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

### Permitir apenas uma lista selecionada

Use isto quando os modelos importados pelo jogador devem ser limitados aos Pals aprovados.

```json
{
    "PalSelectionMode": "AllowOnlyListed",
    "AllowedPalIDs": [
        "Anubis",
        "Kirin",
        "WeaselDragon"
    ],
    "BannedPalIDs": [],
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 50,
    "MaxRank": 4,
    "PalSouls": {
        "Health": 10,
        "Attack": 10,
        "Defense": 10,
        "CraftSpeed": 10
    },
    "IVs": {
        "Health": 80,
        "AttackMelee": 80,
        "AttackShot": 80,
        "Defense": 80
    }
}
```

Nesta configuração, apenas os três valores `PalID` listados podem ser importados. Os valores acima do limite são reduzidos aos máximos configurados e os passivos listados são removidos do Pal.

## Exemplo padrão

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "BannedPalIDs": [
        "JetDragon"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

## Exemplo de substituição por Pal

### `Anubis.json`
```json
{
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "AllowGenderNone": false,
    "MaxLevel": 10,
    "MaxRank": 3,
    "PalSouls": {
        "Health": 5,
        "Attack": 5,
        "Defense": 5,
        "CraftSpeed": 5
    },
    "IVs": {
        "Health": 50,
        "AttackMelee": 50,
        "AttackShot": 50,
        "Defense": 50
    }
}
```
