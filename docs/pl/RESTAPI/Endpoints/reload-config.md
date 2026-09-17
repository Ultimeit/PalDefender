# POST /ReloadConfig



**Punkt końcowy:** `POST /v1/pdapi/ReloadConfig`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Reload.Config`

## Przeznaczenie

Ponownie wczytuje konfigurację PalDefender bez ponownego uruchamiania całego serwera.

## Parametry ścieżki

Brak.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalny pusty obiekt JSON.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/reload-config.md"

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

### Ponowne wczytanie konfiguracji

```http
POST /v1/pdapi/ReloadConfig
```

### Ponowne wczytanie po zmianie tokenów

```http
POST /v1/pdapi/ReloadConfig
```

## Przykładowe zastosowania

- Zastosowanie zmian w obsługiwanych plikach konfiguracyjnych.
- Ponowne wczytanie po aktualizacji `Banlist.json`, reguł importu lub innych plików PalDefender odczytywanych podczas działania serwera.
- Jeśli zmiana nie zadziała po ponownym wczytaniu, uruchom serwer ponownie podczas przerwy technicznej.
