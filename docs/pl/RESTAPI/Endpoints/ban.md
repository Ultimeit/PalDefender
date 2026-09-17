# POST /ban/{player_identifier}



**Punkt końcowy:** `POST /v1/pdapi/ban/<player_identifier>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Punishments.Ban`

## Przeznaczenie

Blokuje użytkownika i zapisuje blokadę w `Banlist.json`. Jeśli użytkownik jest online, może zostać wyrzucony z serwera.

## Parametry ścieżki

- `player_identifier`: `UserId`, `PlayerUID` lub inny obsługiwany identyfikator gracza.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalne pola JSON: tekstowe `Reason` i logiczne `IP`. Ustaw `IP` na `true` tylko wtedy, gdy chcesz zablokować również ustalony adres IP.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/ban.md"

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
| `400` | `IP_UNAVAILABLE` | `IP` miało wartość `true`, ale serwer nie ustalił adresu IP wskazanego użytkownika. |

## Przykłady

### Zablokowanie użytkownika Steam

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Oszustwo związane ze zwrotem płatności"
}
```

### Zablokowanie użytkownika PS5 i jego ustalonego adresu IP

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Omijanie blokady",
    "IP": true
}
```

## Przykładowe zastosowania

- Zablokowanie gracza według `UserId` po sprawdzeniu sprawy przez moderatora.
- Podaj jasny powód, aby inni członkowie zespołu mogli zrozumieć wpis na liście blokad.
- Użyj [GET /banlist](banlist.md), aby sprawdzić aktywny wpis. Dane blokad nie są już zarządzane w `Config.json`.
