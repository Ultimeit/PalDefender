# POST /Broadcast



**Punkt końcowy:** `POST /v1/pdapi/Broadcast`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Messages.Broadcast`

## Przeznaczenie

Wysyła wiadomość na czacie do wszystkich graczy serwera.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z wymaganym polem tekstowym `Message`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/broadcast.md"

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

## Przykłady

### Wysłanie ostrzeżenia o ponownym uruchomieniu

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

## Przykładowe zastosowania

- Zapowiedź zaplanowanej przerwy technicznej.
- Automatyczne wysyłanie wiadomości o rozpoczęciu wydarzenia.
- Użyj [POST /Alert](alert.md), jeśli wiadomość ma być alertem zamiast zwykłej wiadomości na czacie.
