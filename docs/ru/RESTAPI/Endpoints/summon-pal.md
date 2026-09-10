# POST /summon/pal

**Конечная точка:** `POST /v1/pdapi/summon/pal`
**Аутентификация:** Токен носителя
**Разрешение:** `REST.Summon.Pal`

## Цель

Создает Pal в фиксированных координатах карты. Запрос должен предоставить ровно один из `PalID` или `PalTemplate`.

## Тело запроса

| Поле | Тип | Требуется | Описание |
| --- | --- | --- | --- |
| `PalID` | string | Один из | Pal идентификатор вида. Взаимоисключающе с `PalTemplate`. |
| `PalTemplate` | string | Один из | Имя файла из `Pals/Templates/`; использует Pal и уровень шаблона. |
| `X`, `Y`, `Z` | номер | Да | Координаты карты. |
| `Level` | integer | Нет | Уровень для призыва `PalID` (по умолчанию `1`). Игнорируется для шаблона. |
| `Uncapturable` | bool | Нет | Предотвращает захват (по умолчанию `false`). |
| `DisableAI` | bool | Нет | Отключает обычный ИИ (по умолчанию `false`). |
| `DisableDamageMeter` | bool | Нет | Отключает отслеживание повреждений (по умолчанию `false`). |
| `DisableStatuses` | array | Нет | Имена статусов, которые нужно скрыть. |

!!! warning "Миграция максимального HP"
    При использовании `PalTemplate` значение `HP` шаблона становится максимальным HP созданного Pal. `HealthMultiplier` и `HPMultiplier` больше не принимаются в запросах и не возвращаются в ответах; удалите их из существующих REST-интеграций.

## Схема ответа

--8<-- "_snippets/restapi/schemas/summon-pal.md"

## Ошибки

Помимо стандартных ответов `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED` и `REQUEST_TIMEOUT`, этот маршрут может возвращать `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED` или `SUMMON_PAL_FAILED`.

## Пример

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true
}
```
