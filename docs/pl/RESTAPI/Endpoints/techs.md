# GET /techs/{player_identifier}



**Punkt końcowy:** `GET /v1/pdapi/techs/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Techs.Read`

## Przeznaczenie

Wyświetla informacje o technologiach gracza. Identyfikatory można wyszukać na [paldeck.cc/technology](https://paldeck.cc/technology).

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | Nie uzyskano dostępu do wskazanego gracza, jego konta, danych technologii lub tabeli technologii. |
| `500` | `REQUEST_TIMEOUT` | Wewnętrzna funkcja wywołana w wątku gry nie zakończyła się w ciągu 5 sekund. |

## Przykłady

### Odczyt odblokowanych technologii według UserID

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### Odczyt odblokowanych technologii według PlayerUID

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## Przykładowe zastosowania

- Sprawdzanie, czy gracz ma już [`TechID`](https://paldeck.cc/technology), przed odblokowaniem lub usunięciem technologii.
- Tworzenie strony administratora rozróżniającej technologie odblokowane i dostępne.
- Sprawdzanie postępów po udzieleniu pomocy.
