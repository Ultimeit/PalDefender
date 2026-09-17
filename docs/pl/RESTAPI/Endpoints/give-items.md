# POST /give/items/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/give/items/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Items.Give`

## Przeznaczenie

Daje wskazanemu graczowi jeden lub kilka przedmiotów.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z tablicą przyznawanych przedmiotów `Items`. Każdy wpis wymaga [`ItemID`](https://paldeck.cc/items) i dodatniej wartości `Count`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` | Treść nie zawiera tablicy `Items`. |
| `400` | `VALIDATION_FAILED` | Co najmniej jeden wpis przedmiotu jest nieprawidłowy, nieobsługiwany, zbyt duży lub nie mieści się w ekwipunku. |
| `500` | `GRANT_FAILED` | Walidacja zakończyła się pomyślnie, ale serwer nie dodał przedmiotów do ekwipunku. |

## Przykłady

### Przyznanie amunicji i wyrzutni graczowi Steam

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### Przyznanie waluty graczowi PS5

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## Przykładowe zastosowania

- Przyznawanie rekompensat po przywróceniu wcześniejszego zapisu.
- Integracja sklepu, w której zaufana usługa przyznaje zakupione przedmioty.
- Najpierw sprawdź [`ItemID`](https://paldeck.cc/items); nazwy wyświetlane nie zawsze są prawidłowymi identyfikatorami.
