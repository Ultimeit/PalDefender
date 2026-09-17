# POST /deletebase/{base_camp_id}



**Punkt końcowy:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**Uwierzytelnianie:** token Bearer

**Wymagane uprawnienie:** `REST.Base.Delete`

## Przeznaczenie

Usuwa bazę/obóz według identyfikatora obozu bazowego. Jest to działanie administratora niszczące dane.

## Parametry ścieżki

- `base_camp_id`: Identyfikator obozu bazowego, zwykle kopiowany z danych gildii lub bazy.

## Parametry zapytania

Brak.

## Treść żądania

Opcjonalny pusty obiekt JSON. Sprawdź identyfikator przed wysłaniem żądania.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | Wartość `base_camp_id` w ścieżce nie jest prawidłowym GUID. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | Serwer nie uzyskał dostępu do `UPalBaseCampManager`. |
| `404` | `BASE_CAMP_NOT_FOUND` | Nie znaleziono obozu bazowego o podanym GUID. |
| `500` | `DELETE_BASE_FAILED` | Znaleziono obóz bazowy, ale jego zniszczenie lub usunięcie powiązanych danych nie powiodło się. |

## Przykłady

### Usunięcie obozu bazowego według GUID

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### Usunięcie kolejnego obozu bazowego według GUID

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## Przykładowe zastosowania

- Usuwanie opuszczonych lub uszkodzonych baz po sprawdzeniu przez zespół.
- Przed usunięciem ustal właściwy obóz za pomocą [GET /guilds](guilds.md) i [GET /guild](guild.md).
- Nie używaj tego punktu końcowego do rutynowego porządkowania, jeśli procedury zespołu nie obejmują weryfikacji właściciela i kopii zapasowych.
