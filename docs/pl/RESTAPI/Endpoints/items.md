# GET /items/{player_identifier}



**Punkt końcowy:** `GET /v1/pdapi/items/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Items.Read`

## Przeznaczenie

Wyświetla przedmioty wskazanego gracza. Identyfikatory z odpowiedzi można wyszukać na [paldeck.cc/items](https://paldeck.cc/items).

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` | Nie uzyskano dostępu do wskazanego gracza, jego stanu, danych ekwipunku lub wspólnego pojemnika ekwipunku. |
| `500` | `REQUEST_TIMEOUT` | Wewnętrzna funkcja wywołana w wątku gry nie zakończyła się w ciągu 5 sekund. |

## Przykłady

### Odczyt ekwipunku gracza Steam

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### Odczyt ekwipunku gracza GDK

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## Przykładowe zastosowania

- Sprawdzanie ekwipunku przed przyznaniem rekompensaty.
- Sprawdzenie [`ItemID`](https://paldeck.cc/items) przed użyciem [POST /give/items](give-items.md).
- Wyjaśnianie zgłoszeń dotyczących brakujących przedmiotów.
