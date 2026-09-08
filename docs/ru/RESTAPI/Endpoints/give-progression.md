# POST /give/progression/{player_identifier}



**Конечная точка:** `POST /v1/pdapi/give/progression/<player_identifier>`

**Аутентификация:** Токен носителя

**Разрешение:** `REST.Progression.Give`

## Цель

Предоставляет игроку значения прогресса.

## Параметры пути

- `player_identifier`: `UserId` или `PlayerUID` для целевого игрока.

## Параметры запроса

Нет.

## Тело запроса

JSON object с хотя бы одним поддерживаемым разрешением: положительный integer `EXP`, положительный integer `TechnologyPoints`, положительный integer `AncientTechnologyPoints` или `Relics` как непустой object с ключом по типу реликвии с положительные суммы integer.


Поддерживаемые типы реликвий: `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## Схема ответа

--8<-- "_snippets/restapi/schemas/give-progression.md"

## Реакции на ошибки

Тела ошибок используют следующую форму:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP | Код ошибки | Когда это произойдет |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | Заголовок `Authorization` отсутствует, имеет неправильный формат или не соответствует настроенному токену носителя. |
| `403` | `MISSING_PERMISSION` | Токен действителен, но не включает это разрешение конечной точки. |
| `400` | `INVALID_JSON` | Текст запроса был предоставлен, но его не удалось проанализировать как JSON. |
| `400` | `REQUEST_FAILED` | Обратный вызов игрового потока вызвал исключение, или произошел сбой общего преобразователя player/resource. |
| `500` | `REQUEST_TIMEOUT` | Обратный вызов внутреннего игрового потока не завершился в течение 5 секунд. |
| `400` | `INVALID_REQUEST` | Тело не содержит `EXP`, `Relics`, `TechnologyPoints` или `AncientTechnologyPoints`. |
| `400` | `VALIDATION_FAILED` | Указанное значение прогресса отсутствует, не integer, неположительное или необходимые внутренние элементы прогресса недоступны. |

## Примеры

### Дайте EXP игроку GDK

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### Выдавайте очки и реликвии по PlayerUID

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## Сценарии

- Компенсация игрокам после отката сохранения.
- Добавляйте технологические очки, не открывая конкретную технологию.
- Вместо этого используйте [POST /learntech](learntech.md), если вы хотите разблокировать определенный [`TechID`](https://paldeck.cc/technology).
