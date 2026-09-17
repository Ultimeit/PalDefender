# POST /kick/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/kick/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Punishments.Kick`

## Przeznaczenie

Wyrzuca gracza online bez tworzenia wpisu blokady.

## Parametry ścieżki

- `player_identifier`: `UserId`, `PlayerUID` lub inny obsługiwany identyfikator gracza.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalne pole tekstowe JSON: `Reason`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` | Wskazany gracz nie jest online lub nie został znaleziony. |

## Przykłady

### Wyrzucenie gracza GDK z podaniem powodu

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "Bezczynność w obszarze wydarzenia"
}
```

### Wyrzucenie gracza Steam z domyślnym powodem

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## Przykładowe zastosowania

- Wyrzucenie gracza przed przerwą techniczną.
- Wyrzucenie gracza, który utknął, aby mógł połączyć się ponownie.
- Jeśli gracz nie powinien móc wrócić, użyj [POST /ban](ban.md).
