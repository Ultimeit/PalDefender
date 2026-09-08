# 📄 `PalTemplate.json`

используйте <https://paldeck.cc/creator>, чтобы создавать эти файлы намного проще!

!!! tip "поиск по идентификатору"
    Используйте [paldeck.cc/pals](https://paldeck.cc/pals) для `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) для `Passives` и [paldeck.cc/skills](https://paldeck.cc/skills) для `ActiveSkills` и `LearntSkills`.

| Ключ | Тип | Описание                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID` | string | Внутренний идентификатор Pal для создания. Найдите действительные значения [`PalID`](https://paldeck.cc/pals) на Paldeck. |
| `UniqueNPCID` | string | Внутренний идентификатор Pal для создания NPC.                                               |
| `Nickname` | string | Необязательный псевдоним, присвоенный Pal.                                                 |
| `SkinId` | string | Переопределение скина для Pal (используется для индивидуального внешнего вида). Используйте cmd `/getskinids` для получения идентификаторов. |
| `Gender` | string | `"Male"`, `"Female"` или `"None"`.                                                   |
| `Level` | интервал | Уровень pal.                                                               |
| `Exp` | интервал | Очки опыта.                                                                  |
| `Shiny` | bool | Является ли Pal блестящим.                                                           |
| `PartnerSkillLevel` | интервал | Уровень партнерского навыка Pal. Не может быть ниже 1!                           |
| `CondensedPals` | интервал | Количество Pals merged/condensed в этом.                                      |
| `UnusedStatusPoints` | интервал | Доступны статусные баллы для распределения вручную. Вероятно, используется только для игроков?    |
| `FriendshipPoints` | интервал | Значение дружбы для Pal.                                               |
| `PhysicalHealth` | string | Состояние физического здоровья. Допустимые имена: `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick` | string | Состояние болезни работника. Допустимые имена: `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter` | bool | Отмечает Pal как импортированный символ.                                    |
| `HP` / `SP` / `MP` | номер | Базовые значения здоровья, выносливости и маны.                                              |
| `Shield` | номер | Значение щита.                                                              |
| `Hunger` / `MaxHunger` | интервал | Текущее и максимальное значения голода.                                                      |
| `SAN` | интервал | Здравомыслие (психическая устойчивость Pal).                                               |
| `Support` | интервал | Уровень поддержки (используется для поведения и навыков ИИ).                                    |
| `CraftSpeed` | интервал | Множитель скорости крафта.                                                          |
| `PalSouls` | object | Пассивные бонусы души. Содержит: `Health`, `Attack`, `Defense`, `CraftSpeed`. Рекомендуемые нормальные значения контролируются вашими правилами импорта. |
| `IVs` | object | Индивидуальные значения статистики. Содержит: `Health`, `AttackMelee`, `AttackShot`, `Defense`. Рекомендуемые нормальные значения контролируются вашими правилами импорта. |
| `ActiveSkills` | array | Список экипированных навыков. PalDefender 1.9.0 не усекает административные шаблоны PalTemplates до трех записей; каждый вход остается оборудованным. Найдите действительные [идентификаторы навыков](https://paldeck.cc/skills) на Paldeck. Обычное поведение game/UI может по-прежнему предполагать стандартное количество слотов. |
| `LearntSkills` | array | Навыки, которые Pal изучил и на которые может перейти. Избегайте размещения здесь активных навыков. Найдите действительные [идентификаторы навыков](https://paldeck.cc/skills) на Paldeck. |
| `Passives` | array | Пассивные черты, которыми обладает Pal. Обычный Pals должен использовать до 4 пассивных способностей. Найдите действительные значения [`PassiveID`](https://paldeck.cc/passives) на Paldeck. |
| `ExtraWorkSuitabilities` | object | Расширенные типы и уровни работы (например, `"Mining": 2`). Доступные типы работ: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`.  |
| `DisableWorkPreferences` | array | Типы работ, которые Pal отказывается выполнять. Доступные типы работ: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Набор инструкций

1. Создайте по одному файлу JSON для каждого пользовательского Pal в `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Используйте уникальное имя файла, например `RaidRewardAnubis.json`. Команды обычно могут использовать `RaidRewardAnubis` или `RaidRewardAnubis.json`.
3. Всегда включайте `PalID`. Все остальное не является обязательным, но для отсутствующих значений используются значения по умолчанию PalDefender или Palworld.
4. Оставьте `Level` на уровне `1` или выше и `PartnerSkillLevel` на уровне `1` или выше.
5. Put использует атаки в `ActiveSkills` и другие известные атаки в `LearntSkills`. PalDefender больше не перемещает лишние активные записи в изученные навыки.
6. Используйте точные идентификаторы для Pals, навыков, пассивных способностей, скинов и типов работы. Неправильные идентификаторы могут не импортироваться или могут быть проигнорированы.
7. Подтвердите JSON перед загрузкой. JSON не допускает комментариев и завершающих запятых.
8. Если шаблон импортируется, но значения изменяются или блокируются, проверьте `Pals/ImportRules/Default.json` сервера и все файлы переопределения для каждого Pal.

## Пошаговое руководство по настройке

1. Решите, для чего предназначен шаблон: простая награда администратора, босс события, тестовый Pal или шаблон появления для призыва.
2. Выберите `PalID` в [paldeck.cc/pals](https://paldeck.cc/pals). Отображаемое имя не всегда является идентификатором файла, поэтому точно скопируйте идентификатор.
3. Добавляйте только те поля, которыми вы хотите управлять. Короткий шаблон легче отлаживать, чем очень большой.
4. Выберите навыки из [paldeck.cc/skills](https://paldeck.cc/skills). Put использует атаки в `ActiveSkills`; добавьте другие известные атаки в `LearntSkills`.
5. Выберите пассивные умения из [paldeck.cc/passives](https://paldeck.cc/passives). Для обычного использования оставьте до четырех пассивных способностей, если только ваш сервер намеренно не позволяет использовать больше.
6. Сохраните файл в `Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
7. Сначала проверьте `/givemepal_j <filename>`. После этого используйте тот же шаблон для `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, REST, API или `PalSummon.json`.

## Примеры пояснений

В минимальном примере ниже создается Анубис 50-го уровня с тремя экипированными атаками и двумя пассивными способностями. Он подходит для тестирования, поскольку содержит только необходимые `PalID` плюс несколько общих полей.

Более крупный пример намеренно экстремальный. Он показывает доступную структуру для душ, IV, навыков, пассивных способностей и переопределений пригодности к работе. На серверах, использующих правила импорта, высокие значения могут быть ограничены или заблокированы.

## Минимальный пример

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

## Пример

Этот файл должен храниться по адресу: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`.
(`ExamplePalTemplate` может быть любым уникальным именем в этой папке. Это будет аргумент команды для `/givepal_j` и `/spawnpal_j`!)

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
