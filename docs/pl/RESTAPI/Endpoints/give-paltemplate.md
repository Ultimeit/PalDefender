# POST /give/paltemplate/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.PalTemplates.Give`

## Przeznaczenie

Przyznaje jednego lub kilka Pali z plików w `Pals/Templates/`.

## Parametry ścieżki

- `player_identifier`: `UserId` lub `PlayerUID` docelowego gracza.

## Parametry zapytania

Brak.

## Treść żądania

Obiekt JSON z tablicą nazw plików szablonów `PalTemplates`. Dla czytelności można podać rozszerzenie `.json`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | Treść nie zawiera tablicy `PalTemplates`. |
| `400` | `VALIDATION_FAILED` | Co najmniej jedna nazwa szablonu jest nieprawidłowa, import jest niemożliwy lub wynikowe Pale nie mieszczą się w dostępnym miejscu. |

## Przykłady

### Przyznanie graczowi Steam jednego Pala z szablonu

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### Przyznanie graczowi PS5 nagród za rajd z szablonów

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## Przykładowe zastosowania

- Nagrody wymagające określonych umiejętności aktywnych i pasywnych, IV, dusz, pseudonimu lub predyspozycji do pracy.
- Najpierw utwórz szablon zgodnie z opisem [plików PalTemplate](../../FileTypes/PalTemplate.md).
- Reguły importu w `Pals/ImportRules/` mogą blokować lub modyfikować szablony przed przyznaniem Pali.
