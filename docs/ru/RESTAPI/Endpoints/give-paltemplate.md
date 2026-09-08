# POST /give/paltemplate/{player_identifier}



**Конечная точка:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**Аутентификация:** Токен носителя

**Разрешение:** `REST.PalTemplates.Give`

## Цель

Возвращает один или несколько Pals из файлов в `Pals/Templates/`.

## Параметры пути

- `player_identifier`: `UserId` или `PlayerUID` для целевого игрока.

## Параметры запроса

Нет.

## Тело запроса

JSON object с `PalTemplates`, array имен файлов шаблонов. Для ясности можно включить расширение `.json`.

## Схема ответа

--8<-- "_snippets/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | Тело не содержит `PalTemplates` array. |
| `400` | `VALIDATION_FAILED` | Одно или несколько имен файлов шаблонов недействительны, не могут быть импортированы или не помещаются в хранилище Pal. |

## Примеры

### Передайте один шаблон Pal игроку Steam.

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### Раздайте шаблоны наград за рейды игроку PS5.

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## Сценарии

- Используйте, когда для вознаграждений требуются определенные навыки, пассивы, IV, души, прозвище или значения пригодности к работе.
- Используйте [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md), чтобы сначала создать шаблон.
- Правила импорта в `Pals/ImportRules/` могут блокировать или корректировать шаблоны до их предоставления.
