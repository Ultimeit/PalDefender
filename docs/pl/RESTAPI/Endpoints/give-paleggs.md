# POST /give/paleggs/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.PalEggs.Give`

## Przeznaczenie

Daje wskazanemu graczowi jedno lub kilka jaj Pali.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z tablicą przyznawanych jaj `PalEggs`. `EggID` jest identyfikatorem [`ItemID`](https://paldeck.cc/items). Każde jajo musi używać albo [`PalID`](https://paldeck.cc/pals), albo `PalTemplate`, nigdy obu naraz.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | Treść nie zawiera tablicy `PalEggs`. |
| `400` | `VALIDATION_FAILED` | Co najmniej jeden wpis jaja jest nieprawidłowy, nie może zostać zaimportowany lub nie mieści się w ekwipunku. |

## Przykłady

### Przyznanie graczowi Steam jaja z określonym poziomem

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### Przyznanie jaja z szablonu według PlayerUID

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## Przykładowe zastosowania

- Przyznawanie jaj podczas wydarzeń bez natychmiastowego tworzenia Pala.
- Używaj `PalID` dla prostych jaj, a `PalTemplate` dla jaj z niestandardową zawartością.
- Żądanie może się nie powieść, jeśli [`ItemID`](https://paldeck.cc/items) jaja jest błędne lub brakuje miejsca w ekwipunku gracza.
