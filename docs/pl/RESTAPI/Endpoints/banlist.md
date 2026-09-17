# GET /banlist



**Punkt końcowy:** `GET /v1/pdapi/banlist`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Banlist.Read`

## Przeznaczenie

Odczytuje wpisy z listy blokad. Dane blokad są przechowywane w `Banlist.json`, a nie w `Config.json`.

## Parametry ścieżki

Brak.

## Parametry zapytania

- `active`: `true`, `false` lub `1` do filtrowania według stanu aktywności.
- `entryType`: Filtr według typu wpisu blokady.
- `userId`: Filtr według identyfikatora użytkownika.
- `ip` lub `userIP`: Filtr według adresu IP.
- `issuerType`, `issuerName`, `issuerIP`: Filtr według metadanych wystawcy blokady.
- `reason`: Filtr według tekstu powodu.
- `q`: Ogólne wyszukiwanie tekstowe.

## Treść żądania

Brak treści żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/banlist.md"

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

### Wyświetlenie wszystkich wpisów blokad

```http
GET /v1/pdapi/banlist
```

### Wyszukanie aktywnych wpisów użytkownika Steam

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### Wyszukanie wpisów według IP

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## Przykładowe zastosowania

- Sprawdzenie, czy gracz lub adres IP jest obecnie zablokowany.
- Wyszukanie według powodu lub wystawcy przed cofnięciem blokady.
- Utworzenie panelu moderacji odczytującego `Banlist.json` przez API.

## Powiązane strony

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), a także [POST /unbanip](unbanip.md).
