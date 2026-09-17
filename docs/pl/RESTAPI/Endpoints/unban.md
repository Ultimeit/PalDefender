# POST /unban/{user_id}



**Punkt końcowy:** `POST /v1/pdapi/unban/<user_id>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Punishments.Unban`

## Przeznaczenie

Cofa blokadę identyfikatora użytkownika w `Banlist.json`.

## Parametry ścieżki

- `user_id`: Identyfikator użytkownika, którego blokadę należy cofnąć.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalne pole tekstowe JSON: `Reason`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/unban.md"

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
| `400` | `INVALID_JSON` | Przesłano treść żądania, ale nie można jej odczytać jako JSON. |
| `400` | `REQUEST_FAILED` | Funkcja wywołana w wątku gry zgłosiła wyjątek lub wspólny mechanizm wyszukiwania gracza/zasobu zakończył się niepowodzeniem. |
| `500` | `REQUEST_TIMEOUT` | Wewnętrzna funkcja wywołana w wątku gry nie zakończyła się w ciągu 5 sekund. |
| `400` | `VALIDATION_FAILED` | Opcjonalne pole żądania ma nieprawidłowy typ JSON. |
| `404` | `BAN_NOT_FOUND` | Podany `user_id` nie ma aktywnej blokady. |

## Przykłady

### Cofnięcie blokady użytkownika Steam

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Odwołanie przyjęte"
}
```

### Cofnięcie blokady użytkownika PS5 z domyślnym powodem

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## Przykładowe zastosowania

- Cofnięcie blokady użytkownika po uwzględnieniu odwołania.
- Zapisz powód na potrzeby późniejszej kontroli.
- Użyj [GET /banlist](banlist.md) z `userId` lub `q`, aby sprawdzić wynik.
