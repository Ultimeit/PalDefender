# POST /learntech/{player_identifier}



**Конечная точка:** `POST /v1/pdapi/learntech/<player_identifier>`

**Аутентификация:** Токен носителя

**Разрешение:** `REST.Techs.Learn`

## Цель

Изучает одну, несколько или все технологии игрока.

## Параметры пути

- `player_identifier`: `UserId` или `PlayerUID` для целевого игрока.

## Параметры запроса

Нет.

## Тело запроса

`Technology` может быть одним [`TechID`](https://paldeck.cc/technology), string `"All"` или array значений [`TechID`](https://paldeck.cc/technology). Не помещайте `"All"` внутрь array.

## Схема ответа

--8<-- "_snippets/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` отсутствует или не является string/array в ожидаемом формате. |
| `400` | `VALIDATION_FAILED` | `Technology` array содержит не-string, `All` или неверный технологический идентификатор. |

## Примеры

### Изучите одну технологию для игрока Steam

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Изучите несколько технологий для плеера PS5.

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Изучите каждую технологию с помощью PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Сценарии

- Разблокируйте недостающий рецепт поддержки.
- Разблокируйте все технологии для тестовых аккаунтов.
- Перед отправкой запроса проверьте идентификаторы технологий в [paldeck.cc/technology](https://paldeck.cc/technology).
