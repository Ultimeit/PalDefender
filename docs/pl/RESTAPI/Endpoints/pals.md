# GET /pals/{player_identifier}



**Punkt końcowy:** `GET /v1/pdapi/pals/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Pals.Read`

## Przeznaczenie

Wyświetla Pale wskazanego gracza. Identyfikatory z odpowiedzi można wyszukać na [paldeck.cc/pals](https://paldeck.cc/pals).

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/pals.md"

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
| `404` | `PLAYER_STATE_NOT_FOUND` | Gracz istnieje, ale jego `APalPlayerState` jest niedostępny. |

## Przykłady

### Odczyt Pali gracza PS5

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### Odczyt Pali według PlayerUID

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## Przykładowe zastosowania

- Sprawdzanie gracza przed udzieleniem pomocy.
- Sprawdzenie otrzymania Pala po użyciu [POST /give/pals](give-pals.md) lub [POST /give/paltemplate](give-paltemplate.md).
- Wyjaśnianie zgłoszeń dotyczących brakujących lub nieoczekiwanych Pali.
