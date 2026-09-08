# 📄 `Pals/ImportRules/*.json`


Правила импорта Pal определяют, какие файлы `PalTemplate.json` разрешены, заблокированы или изменены при импорте с помощью команд или действий API.

!!! tip "поиск по идентификатору"
    Используйте [paldeck.cc/pals](https://paldeck.cc/pals) для имен файлов `AllowedPalIDs`, `BannedPalIDs` и для каждого правила Pal. Используйте [paldeck.cc/passives](https://paldeck.cc/passives) для `DisallowedPassives`.

## Расположение файлов

| Файл | Цель |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | Глобальные правила импорта для всех шаблонов Pal. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | Необязательное переопределение для каждого Pal. Найдите [`PalID`](https://paldeck.cc/pals) на Paldeck, а затем используйте этот точный идентификатор в качестве имени файла. Пример: `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | Пример файла, созданного для справки. Это не настоящее правило Pal, пока оно не будет скопировано и переименовано. |

## Ключи

| Ключ | Тип | Описание |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | Только `Default.json`. `AllowAllExceptBanned` допускает все Pal, кроме `BannedPalIDs`. `AllowOnlyListed` допускает только `AllowedPalIDs`. |
| `AllowedPalIDs` | array | Только `Default.json`. Значения [`PalID`](https://paldeck.cc/pals) разрешены, если `PalSelectionMode` равен `AllowOnlyListed`. |
| `BannedPalIDs` | array | Только `Default.json`. [`PalID`](https://paldeck.cc/pals) значения, которые всегда отвергаются. |
| `MaxValueLimitAction` | string | `BlockImport` запрещает использование шаблонов, превышающих установленные ограничения. `ClampToMaxValues` снижает значения до настроенных пределов. |
| `DisallowedPassivesAction` | string | `BlockImport` запрещает шаблоны с указанными пассивными способностями. `RemoveFromPal` удаляет перечисленные пассивные способности перед импортом. |
| `DisallowedPassives` | array | Значения [`PassiveID`](https://paldeck.cc/passives), на которые влияет `DisallowedPassivesAction`. |
| `ConditionMode` | string | `None` применяет правило обычным образом. `RequirePalCaptureCount` позволяет импортировать Pal только после того, как этот игрок поймал достаточное количество Pals того же вида. |
| `RequiredCaptureCount` | интервал | Обязательное количество отловов представителей одного вида, если `ConditionMode` равен `RequirePalCaptureCount` (по умолчанию `5`). |
| `Disabled` | bool | Если `true`, отключает проверки импорта для соответствующего набора правил. |
| `BanIfPalIsImpossible` | bool | Если `true`, PalDefender может наказывать невозможный импорт Pal в соответствии с настройками сервера. |
| `AllowGenderNone` | bool | Если `false`, шаблоны, использующие `Gender: "None"`, могут быть отклонены при проверке импорта. |
| `MaxLevel` | интервал | Максимально допустимый уровень Pal для импортированных шаблонов. |
| `MaxRank` | интервал | Максимально допустимый уровень квалификации партнера для импортированных шаблонов. |
| `PalSouls` | object | Максимально допустимые значения души Pal: `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | object | Максимально допустимые значения IV: `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## Набор инструкций

1. Начните с `Default.json`. Используйте его для политики всего сервера.
2. Используйте файлы per-Pal только в том случае, если для одного Pal требуются разные ограничения.
3. Файлы Per-Pal должны иметь идентификатор Pal, например `Anubis.json`.
4. Не помещайте `PalSelectionMode`, `AllowedPalIDs` или `BannedPalIDs` в файлы правил для отдельных Pal. Эти ключи должны находиться в `Default.json`.
5. Используйте `BlockImport`, если хотите строгую модерацию.
6. Используйте `ClampToMaxValues`, если вы предпочитаете принимать шаблоны, но уменьшать значения превышения предела.
7. Используйте `RemoveFromPal` для пассивных элементов, если вы предпочитаете автоматическую очистку неудачному импорту.
8. Соблюдайте точность идентификаторов и проверяйте JSON перед загрузкой.

## Пошаговое руководство по настройке

1. Откройте или создайте `Pals/ImportRules/Default.json`.
2. Определите глобальную политику Pal:
   - Используйте `AllowAllExceptBanned`, если разрешено большинство Pals, и вы хотите заблокировать только некоторые.
   - Используйте `AllowOnlyListed`, если импорт должен быть ограничен курируемым списком.
3. Определите стиль модерации:
   - Используйте `BlockImport` для строгих серверов, на которых недействительные шаблоны должны давать сбой.
   - Используйте `ClampToMaxValues`, если вы хотите принять шаблоны, но уменьшить превышение лимита уровней, рангов, душ или IV.
   - Используйте `RemoveFromPal` для пассивных элементов, если вы хотите удалить ненужные пассивные элементы вместо того, чтобы отклонять весь шаблон.
4. Добавьте запрещенные пассивные способности из [paldeck.cc/passives](https://paldeck.cc/passives).
5. Добавьте запрещенный или разрешенный Pals из [paldeck.cc/pals](https://paldeck.cc/pals).
6. Добавляйте переопределение для каждого Pal только в том случае, если для конкретного Pal требуются более строгие или более свободные ограничения, чем для глобального файла.
7. Прежде чем импортировать большие шаблоны, сначала протестируйте небольшой `PalTemplate.json`.

## Общие настройки

### Разрешить большую часть Pals, заблокировать некоторые

Используйте это, когда разрешены обычные награды администратора, но некоторые Pals не следует импортировать.

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

### Разрешить только курируемый список

Используйте это, когда шаблоны, импортированные игроком, должны быть ограничены утвержденным Pals.

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

В этой настройке можно импортировать только три перечисленных значения `PalID`. Значения сверхпредела уменьшаются до настроенных максимумов, а перечисленные пассивные способности удаляются из Pal.

## Пример по умолчанию

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

## Пример переопределения для каждого-Pal

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
