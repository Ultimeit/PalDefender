# POST /give/paleggs/{player_identifier}



**Конечная точка:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**Аутентификация:** Токен носителя

**Разрешение:** `REST.PalEggs.Give`

## Цель

Дает одно или несколько яиц Pal целевому игроку.

## Параметры пути

- `player_identifier`: `UserId` или `PlayerUID` для целевого игрока.

## Параметры запроса

Нет.

## Тело запроса

JSON object с `PalEggs`, array яичных грантов. `EggID` — это [`ItemID`](https://paldeck.cc/items). Каждое яйцо должно использовать либо [`PalID`](https://paldeck.cc/pals), либо `PalTemplate`, но не оба.

## Схема ответа

--8<-- "_snippets/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | Тело не содержит `PalEggs` array. |
| `400` | `VALIDATION_FAILED` | Один или несколько грантов на яйца недействительны, не могут быть импортированы или не помещаются в инвентарь. |

## Примеры

### Дайте уровневое яйцо игроку Steam.

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### Дайте яйцо на основе шаблона от PlayerUID

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## Сценарии

- Дайте яйца событий, не создавая Pal немедленно.
- Используйте `PalID` для простых яиц и `PalTemplate` для пользовательского содержимого яиц.
- Запрос может завершиться неудачей, если яйцо [`ItemID`](https://paldeck.cc/items) недействительно или в инвентаре игрока нет места.
