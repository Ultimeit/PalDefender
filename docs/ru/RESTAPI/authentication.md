# Аутентификация и настройка

## Включение API

1. Открыто: `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Установите для `"Enabled"` значение `true`.
3. Перезапустите сервер.

При запуске вы должны увидеть журналы, похожие на:
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Loaded 1 Bearer token.
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Порт

- **Порт по умолчанию:** `17993`

**Не открывайте API для публичного доступа.** Если доступ к API нужен за пределами локальной сети или компьютера, разместите его за **обратным прокси-сервером** (nginx/Caddy/Traefik) и завершайте TLS там. Сам REST API PalDefender должен оставаться привязанным к localhost или частному интерфейсу.

## Токены

- Запустите сервер один раз, чтобы сгенерировать пример токена.
- Каждый файл `.json` внутри `Win64/PalDefender/RESTAPI/Tokens/` рассматривается как действительный файл токена. (Единственным исключением является файл `TokenExample.json`!)
- Создайте **один токен для каждого person/service**.. Токены — это пароли.

Пример файла токена:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

    `Permissions` может быть строкой string или array. Используйте более узкие разрешения для общедоступных информационных панелей или автоматизации, которые не должны иметь полный доступ администратора.

## Заголовки
Отправьте токен через стандартный заголовок авторизации:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python пример
```py
import requests

base_url = "http://127.0.0.1:17993"
# do not do this. Never store the token in any code. use smth like .env! This is only for demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
