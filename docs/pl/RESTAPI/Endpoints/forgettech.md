# POST /forgettech/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/forgettech/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Techs.Forget`

## Przeznaczenie

Usuwa jedną, kilka lub wszystkie poznane technologie gracza.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

`Technology` może być pojedynczym [`TechID`](https://paldeck.cc/technology), ciągiem znaków `"All"` lub tablicą ciągów [`TechID`](https://paldeck.cc/technology). Nie umieszczaj `"All"` w tablicy.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/forgettech.md"

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
| `400` | `INVALID_REQUEST` | Brakuje `Technology` lub nie jest ono ciągiem znaków ani tablicą w oczekiwanym formacie. |
| `400` | `VALIDATION_FAILED` | Tablica `Technology` zawiera wartość inną niż ciąg znaków, `All` lub nieprawidłowy identyfikator technologii. |

## Przykłady

### Usunięcie jednej technologii gracza GDK

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Usunięcie kilku technologii według PlayerUID

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Usunięcie wszystkich technologii gracza Steam

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Przykładowe zastosowania

- Usunięcie technologii przyznanej przez pomyłkę.
- Zresetowanie konta testowego za pomocą `"All"`.
- Sprawdź stan przed żądaniem i po nim za pomocą [GET /techs](techs.md).
