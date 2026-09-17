# POST /learntech/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/learntech/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Techs.Learn`

## Przeznaczenie

Odblokowuje graczowi jedną, kilka lub wszystkie technologie.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

`Technology` może być pojedynczym [`TechID`](https://paldeck.cc/technology), ciągiem znaków `"All"` lub tablicą ciągów [`TechID`](https://paldeck.cc/technology). Nie umieszczaj `"All"` w tablicy.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/learntech.md"

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

### Odblokowanie jednej technologii graczowi Steam

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Odblokowanie kilku technologii graczowi PS5

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Odblokowanie wszystkich technologii według PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Przykładowe zastosowania

- Odblokowanie brakującej receptury w ramach pomocy graczowi.
- Odblokowanie wszystkich technologii na kontach testowych.
- Przed wysłaniem żądania sprawdź identyfikatory technologii na [paldeck.cc/technology](https://paldeck.cc/technology).
