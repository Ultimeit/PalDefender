# POST /unbanip/{ip}



**Punkt końcowy:** `POST /v1/pdapi/unbanip/<ip>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Punishments.UnbanIP`

## Przeznaczenie

Cofa blokadę adresu IP w `Banlist.json`.

## Parametry ścieżki

- `ip`: Adres IP, którego blokadę należy cofnąć.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalne pole tekstowe JSON: `Reason`.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/unbanip.md"

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
| `404` | `BAN_NOT_FOUND` | Podany `ip` nie ma aktywnej blokady. |

## Przykłady

### Cofnięcie blokady IP z podaniem powodu

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Tymczasowa blokada wygasła"
}
```

### Cofnięcie blokady IP z domyślnym powodem

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## Przykładowe zastosowania

- Cofnięcie blokady IP po wyjaśnieniu sprawy.
- Użyj, gdy gracz nadal nie może wejść po cofnięciu blokady użytkownika, ponieważ wpis blokady IP pozostaje aktywny.
- Użyj [GET /banlist](banlist.md) z `ip`, aby sprawdzić wynik.
