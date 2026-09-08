# POST /SendPlayerMessage



**Конечная точка:** `POST /v1/pdapi/SendPlayerMessage`

**Аутентификация:** Токен носителя

**Разрешение:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## Цель

Отправляет сообщение одному или нескольким целевым игрокам.

## Параметры пути

Нет.

## Параметры запроса

Нет.

## Тело запроса

JSON object с `SendType`, `Message` и `UserID` или `UserIDs`. Общие значения `SendType` включают `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant` и `PlayerLogVeryImportant`.

## Схема ответа

--8<-- "_snippets/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` | Тело запроса пусто. |
| `400` | `INVALID_JSON` | Недопустимое тело запроса JSON. |
| `400` | `VALIDATION_FAILED` | `SendType`, `Message`, `UserID` или `UserIDs` отсутствует, пуст, дублируется или имеет неверный тип. |
| `400` | `PLAYER_NOT_FOUND` | Не удалось найти один или несколько целевых идентификаторов пользователей или UID игроков. |
| `400` | `SEND_MESSAGE_FAILED` | Проверка пройдена, но сервер отклонил операцию отправки сообщения. |
| `400` | `REQUEST_FAILED` | Обратный вызов игрового потока вызвал исключение. |
| `500` | `REQUEST_TIMEOUT` | Обратный вызов внутреннего игрового потока не завершился в течение 5 секунд. |

## Примеры

### Отправить чат игрока одному пользователю

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived."
}
```

### Отправить важный журнал смешанным целям

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "The event starts in 10 minutes."
}
```

## Сценарии

- Отправляйте предупреждения о перезапуске выбранным игрокам.
- Отправляйте ответы в службу поддержки из панели администратора.
- Используйте `UserID` для одной цели и `UserIDs` для нескольких целей, а не обе.
