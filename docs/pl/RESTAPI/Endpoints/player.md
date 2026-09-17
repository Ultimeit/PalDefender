# GET /player/{player_identifier}



**Punkt końcowy:** `GET /v1/pdapi/player/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Player.Read`

## Przeznaczenie

Zwraca dane jednego gracza. Można użyć obsługiwanego identyfikatora, takiego jak `UserId` lub `PlayerUID`.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/player.md"

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
| `404` | `PLAYER_NOT_FOUND` | Nie znaleziono gracza online o podanym `player_identifier`. |
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | Znaleziono gracza, ale nie udało się wczytać danych jego konta. |

## Przykłady

### Wyszukiwanie według UserID Steam

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### Wyszukiwanie według PlayerUID

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## Przykładowe zastosowania

- Otwarcie szczegółów gracza po wybraniu wiersza z `GET /players`.
- Sprawdzanie celu przed przyznaniem nagród lub nałożeniem kar.
- Sprawdzanie, czy serwer może obecnie odnaleźć gracza.
