# POST /forgettech/{player_identifier}



**Конечная точка:** `POST /v1/pdapi/forgettech/<player_identifier>`

**Аутентификация:** Токен носителя

**Разрешение:** `REST.Techs.Forget`

## Цель

Забывает одну, несколько или все технологии игрока.

## Параметры пути

- `player_identifier`: `UserId` или `PlayerUID` для целевого игрока.

## Параметры запроса

Нет.

## Тело запроса

`Technology` может быть одним [`TechID`](https://paldeck.cc/technology), string `"All"` или array значений [`TechID`](https://paldeck.cc/technology). Не помещайте `"All"` внутрь array.

## Схема ответа

--8<-- "_snippets/restapi/schemas/forgettech.md"

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

### Забудьте одну технологию для игрока GDK

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Забудьте о некоторых технологиях PlayerUID

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Забудьте все технологии для игрока Steam

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Сценарии

- Удалить технологию, предоставленную по ошибке.
- Сбросьте тестовую учетную запись с помощью `"All"`.
- Подтвердите текущее состояние с помощью [GET /techs](techs.md) до и после запроса.
