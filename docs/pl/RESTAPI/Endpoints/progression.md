# GET /progression/{player_identifier}



**Punkt końcowy:** `GET /v1/pdapi/progression/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Progression.Read`

## Przeznaczenie

Odczytuje postępy gracza, takie jak EXP, stan związany z poziomem, sumy punktów reliktów i technologii.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` | Nie uzyskano dostępu do wskazanego gracza, konta, indywidualnych danych postaci, danych zapisu lub technologii. |
| `500` | `REQUEST_TIMEOUT` | Wewnętrzna funkcja wywołana w wątku gry nie zakończyła się w ciągu 5 sekund. |

## Przykłady

### Odczyt postępów według UserID PS5

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### Odczyt postępów według PlayerUID

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Przykładowe zastosowania

- Sprawdzanie bieżących wartości przed przyznaniem postępów.
- Sprawdzanie efektów pomocy po [POST /give/progression](give-progression.md).
- Tworzenie podsumowania gracza w zaufanym panelu administratora.
