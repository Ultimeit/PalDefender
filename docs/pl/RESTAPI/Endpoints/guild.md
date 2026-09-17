# GET /guild/{guild_id}



**Punkt końcowy:** `GET /v1/pdapi/guild/<guild_id>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Guild.Read`

## Przeznaczenie

Zwraca jedną gildię ze szczegółowymi informacjami o członkach i bazach/obozach.

## Parametry ścieżki

- `guild_id`: Identyfikator gildii, zwykle kopiowany z [GET /guilds](guilds.md).

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` | Nie znaleziono gildii o podanym `guild_id`. |

## Przykłady

### Odczyt członków i obozów gildii

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### Odczyt kolejnej gildii według GUID

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Przykładowe zastosowania

- Sprawdzanie właściciela bazy przed jej usunięciem.
- Sprawdzanie członków gildii i danych obozów podczas obsługi zgłoszeń.
- Ostrożnie używaj identyfikatorów obozów z odpowiedzi w [POST /deletebase](deletebase.md).
