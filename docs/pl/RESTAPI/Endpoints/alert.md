# POST /Alert



**Punkt końcowy:** `POST /v1/pdapi/Alert`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Messages.Alert`

## Przeznaczenie

Wysyła alert do graczy na serwerze.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z polem tekstowym `Message`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/alert.md"

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
| `400` | `VALIDATION_FAILED` | Brakuje `Message`, pole jest puste lub nie jest ciągiem znaków. |
| `400` | `BROADCAST_ALERT_FAILED` | Serwer nie zdołał wysłać alertu. |

## Przykłady

### Wysłanie alertu o ponownym uruchomieniu

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Ponowne uruchomienie teraz."
}
```

### Wysłanie alertu wielowierszowego

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Ponowne uruchomienie serwera za 5 minut.\nWróć do bazy."
}
```

## Przykładowe zastosowania

- Wysyłanie pilnych ostrzeżeń serwera.
- Wysłanie końcowego, pilnego przypomnienia po wiadomości ogólnej.
- Alerty powinny być krótkie, aby łatwo było je przeczytać w grze.
