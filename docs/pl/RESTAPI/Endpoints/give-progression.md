# POST /give/progression/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/give/progression/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Progression.Give`

## Przeznaczenie

Przyznaje graczowi postępy.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z co najmniej jedną obsługiwaną nagrodą: dodatnią liczbą całkowitą `EXP`, `TechnologyPoints` lub `AncientTechnologyPoints`, albo niepustym obiektem `Relics`, którego klucze oznaczają typy reliktów, a wartości są dodatnimi liczbami całkowitymi.


Obsługiwane typy reliktów: `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/give-progression.md"

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
| `400` | `INVALID_REQUEST` | Treść nie zawiera żadnego z pól `EXP`, `Relics`, `TechnologyPoints` ani `AncientTechnologyPoints`. |
| `400` | `VALIDATION_FAILED` | Brakuje wymaganej wartości postępów, wartość nie jest dodatnią liczbą całkowitą lub wewnętrzne dane postępów są niedostępne. |

## Przykłady

### Przyznanie EXP graczowi GDK

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### Przyznanie punktów i reliktów według PlayerUID

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## Przykładowe zastosowania

- Rekompensaty dla graczy po przywróceniu wcześniejszego zapisu.
- Dodawanie punktów technologii bez odblokowania określonej technologii.
- Aby odblokować określone [`TechID`](https://paldeck.cc/technology), użyj [POST /learntech](learntech.md).
