# GET /players



**Punkt końcowy:** `GET /v1/pdapi/players`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Players.Read`

## Przeznaczenie

Wyświetla znanych graczy wraz z identyfikatorami i informacjami o stanie. Przydaje się do tworzenia list wyboru graczy w narzędziach administratora.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | Serwer nie uzyskał dostępu do menedżera graczy Palworld. |

## Przykłady

### Wyświetlenie wszystkich znanych graczy

```http
GET /v1/pdapi/players
```

### Odświeżenie listy wyboru graczy administratora

```http
GET /v1/pdapi/players
```

## Przykładowe zastosowania

- Tworzenie listy rozwijanej graczy online i znanych graczy.
- Wyszukanie właściwego `UserId` lub `PlayerUID` przed wywołaniem punktów końcowych nagród, kar lub ekwipunku.
- Sprawdzanie obecności graczy przed wysłaniem wiadomości lub ostrzeżenia o przerwie technicznej.

## Powiązane strony

- [GET /player](player.md) — dane jednego gracza.
- [POST /kick](kick.md), [POST /ban](ban.md) i punkty końcowe nagród używają tego samego rodzaju identyfikatorów graczy.
