# POST /summon/pal

**Punkt końcowy:** `POST /v1/pdapi/summon/pal`  
**Uwierzytelnianie:** token Bearer  
**Wymagane uprawnienie:** `REST.Summon.Pal`

## Przeznaczenie

Tworzy Pala pod określonymi współrzędnymi mapy. Żądanie musi zawierać dokładnie jedno z pól: `PalID` lub `PalTemplate`.

## Treść żądania

| Pole | Typ | Wymagane | Opis |
| --- | --- | --- | --- |
| `PalID` | ciąg znaków | Jedno z dwóch | Identyfikator gatunku Pala. Nie można podawać razem z `PalTemplate`. |
| `PalTemplate` | ciąg znaków | Jedno z dwóch | Nazwa pliku z `Pals/Templates/`; używa Pala i poziomu z szablonu. |
| `X`, `Y`, `Z` | liczba | Tak | Współrzędne mapy. |
| `Level` | liczba całkowita | Nie | Poziom przywołań według `PalID` (domyślnie `1`). Ignorowany przy użyciu szablonu. |
| `Uncapturable` | wartość logiczna | Nie | Uniemożliwia schwytanie (domyślnie `false`). |
| `DisableAI` | wartość logiczna | Nie | Wyłącza zwykłą sztuczną inteligencję (domyślnie `false`). |
| `DisableDamageMeter` | wartość logiczna | Nie | Wyłącza śledzenie obrażeń (domyślnie `false`). |
| `DisableStatuses` | tablica | Nie | Nazwy efektów statusu do zablokowania. |

!!! warning "Migracja maksymalnego HP"
    Przy użyciu `PalTemplate` wartość `HP` szablonu staje się maksymalnym HP utworzonego Pala. `HealthMultiplier` i `HPMultiplier` nie są już przyjmowane w żądaniach ani zwracane w odpowiedziach; usuń je z istniejących integracji REST.

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/summon-pal.md"

## Błędy

Oprócz standardowych odpowiedzi `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED` i `REQUEST_TIMEOUT` ta ścieżka może zwrócić `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED` lub `SUMMON_PAL_FAILED`.

## Przykład

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true
}
```
