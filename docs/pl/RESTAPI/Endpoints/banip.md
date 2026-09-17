# POST /banip/{ip}



**Punkt końcowy:** `POST /v1/pdapi/banip/<ip>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Punishments.BanIP`

## Przeznaczenie

Blokuje adres IP i zapisuje blokadę w `Banlist.json`.

## Parametry ścieżki

- `ip`: Adres IP do zablokowania.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalne pola tekstowe JSON: `Reason` i `UserId`, gdy blokada IP ma być powiązana z użytkownikiem.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/banip.md"

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

## Przykłady

### Zablokowanie samego adresu IP

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Ruch botów"
}
```

### Zablokowanie adresu IP i powiązanie użytkownika GDK

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Nadużycia z użyciem dodatkowego konta",
    "UserId": "gdk_2533274898765432"
}
```

## Przykładowe zastosowania

- Zatrzymanie powtarzających się nadużyć z tego samego IP po sprawdzeniu przez zespół.
- Jeśli znasz `UserId`, powiąż go z blokadą, aby ułatwić kontrolę wpisów.
- Użyj [GET /banlist](banlist.md) z `ip`, aby sprawdzić aktywny wpis.
