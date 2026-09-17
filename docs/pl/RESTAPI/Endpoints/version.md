# GET /version



**Punkt końcowy:** `GET /v1/pdapi/version`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Version.Read`

## Przeznaczenie

Używaj tego punktu końcowego do sprawdzania dostępności i wersji w narzędziach, panelach i skryptach.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/version.md"

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

## Przykłady

### Sprawdzenie dostępności i wersji

```http
GET /v1/pdapi/version
```

## Przykładowe zastosowania

- Po skonfigurowaniu tokenu REST API sprawdź nim działanie uwierzytelniania.
- Wywołaj go przed innymi punktami końcowymi, jeśli narzędzie wymaga określonej minimalnej wersji PalDefender.
- Używaj go do monitorowania, ponieważ jest najmniejszym żądaniem tylko do odczytu.
