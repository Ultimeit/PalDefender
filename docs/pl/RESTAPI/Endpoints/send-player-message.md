# POST /SendPlayerMessage



**Punkt końcowy:** `POST /v1/pdapi/SendPlayerMessage`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## Przeznaczenie

Wysyła wiadomość do jednego lub kilku wskazanych graczy.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z `SendType`, `Message` oraz `UserID` albo `UserIDs`. Typowe wartości `SendType` to `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant` i `PlayerLogVeryImportant`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/send-player-message.md"

## Odpowiedzi błędów

Treść odpowiedzi błędu ma następującą postać:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Czytelny opis błędu",
        "Details": {}
    }
}
```

| HTTP | Kod błędu | Kiedy występuje |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | Brakuje nagłówka `Authorization`, ma on nieprawidłowy format lub nie odpowiada żadnemu skonfigurowanemu tokenowi Bearer. |
| `403` | `MISSING_PERMISSION` | Token jest prawidłowy, ale nie ma uprawnienia wymaganego przez ten punkt końcowy. |
| `400` | `EMPTY_BODY` | Treść żądania jest pusta. |
| `400` | `INVALID_JSON` | Treść żądania nie jest prawidłowym JSON. |
| `400` | `VALIDATION_FAILED` | Brakuje `SendType`, `Message`, `UserID` lub `UserIDs`, pole jest puste, powielone albo ma nieprawidłowy typ. |
| `400` | `PLAYER_NOT_FOUND` | Nie znaleziono co najmniej jednego wskazanego identyfikatora użytkownika lub UID gracza. |
| `400` | `SEND_MESSAGE_FAILED` | Walidacja zakończyła się pomyślnie, ale serwer odrzucił wysłanie wiadomości. |
| `400` | `REQUEST_FAILED` | Funkcja wywołana w wątku gry zgłosiła wyjątek. |
| `500` | `REQUEST_TIMEOUT` | Wewnętrzna funkcja wywołana w wątku gry nie zakończyła się w ciągu 5 sekund. |

## Przykłady

### Wysłanie wiadomości na czacie do jednego użytkownika

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Twoje zamówienie ze sklepu dotarło."
}
```

### Wysłanie ważnego komunikatu do odbiorców z różnymi typami identyfikatorów

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
    "Message": "Wydarzenie rozpocznie się za 10 minut."
}
```

## Przykładowe zastosowania

- Wysyłanie wybranym graczom bezpośrednich ostrzeżeń o ponownym uruchomieniu.
- Wysyłanie odpowiedzi pomocy technicznej z panelu administratora.
- Używaj `UserID` dla jednego odbiorcy lub `UserIDs` dla kilku; nie podawaj obu pól naraz.
