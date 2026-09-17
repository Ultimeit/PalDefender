# GET /guilds



**Punkt końcowy:** `GET /v1/pdapi/guilds`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Guilds.Read`

## Przeznaczenie

Wyświetla znane gildie z podstawowymi informacjami. Użyj tego punktu końcowego, aby poznać identyfikatory przed pobraniem danych konkretnej gildii.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/guilds.md"

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

## Przykłady

### Wyświetlenie wszystkich gildii

```http
GET /v1/pdapi/guilds
```

### Odświeżenie danych panelu gildii

```http
GET /v1/pdapi/guilds
```

## Przykładowe zastosowania

- Utworzenie listy wyboru gildii w panelu administratora.
- Wyszukanie `guild_id` dla [GET /guild](guild.md).
- Szybkie sprawdzanie liczby baz, członków i właścicieli gildii.
