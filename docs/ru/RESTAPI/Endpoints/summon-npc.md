# POST /summon/npc

**Конечная точка:** `POST /v1/pdapi/summon/npc`
**Аутентификация:** Токен носителя
**Разрешение:** `REST.Summon.NPC`

## Цель

Создает NPC в фиксированных координатах карты.

## Тело запроса

| Поле | Тип | Требуется | Описание |
| --- | --- | --- | --- |
| `NPCID` | string | Да | Идентификатор NPC или идентификатор символа NPC. |
| `X`, `Y`, `Z` | номер | Да | Координаты карты. |
| `Level` | integer | Нет | Уровень NPC (по умолчанию `1`). |
| `Uncapturable` | bool | Нет | Предотвращает захват (по умолчанию `false`). |
| `DisableAI` | bool | Нет | Отключает обычный ИИ (по умолчанию `false`). |

## Схема ответа

--8<-- "_snippets/restapi/schemas/summon-npc.md"

## Ошибки

Помимо стандартных ошибок authentication/request, этот маршрут может возвращать `VALIDATION_FAILED` или `SUMMON_NPC_FAILED`.

## Пример

```http
POST /v1/pdapi/summon/npc
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "NPCID": "PIDF_Soldier_AssaultRifle",
    "Level": 30,
    "X": 230,
    "Y": -486,
    "Z": 4097
}
```
