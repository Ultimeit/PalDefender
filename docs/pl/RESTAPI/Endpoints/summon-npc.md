# POST /summon/npc

**Punkt końcowy:** `POST /v1/pdapi/summon/npc`  
**Uwierzytelnianie:** token Bearer  
**Wymagane uprawnienie:** `REST.Summon.NPC`

## Przeznaczenie

Tworzy NPC pod określonymi współrzędnymi mapy.

## Treść żądania

| Pole | Typ | Wymagane | Opis |
| --- | --- | --- | --- |
| `NPCID` | ciąg znaków | Tak | Identyfikator NPC lub postaci NPC. |
| `X`, `Y`, `Z` | liczba | Tak | Współrzędne mapy. |
| `Level` | liczba całkowita | Nie | Poziom NPC (domyślnie `1`). |
| `Uncapturable` | wartość logiczna | Nie | Uniemożliwia schwytanie (domyślnie `false`). |
| `DisableAI` | wartość logiczna | Nie | Wyłącza zwykłą sztuczną inteligencję (domyślnie `false`). |

## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/summon-npc.md"

## Błędy

Oprócz standardowych błędów uwierzytelniania i żądania ta ścieżka może zwrócić `VALIDATION_FAILED` lub `SUMMON_NPC_FAILED`.

## Przykład

```http
POST /v1/pdapi/summon/npc
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "NPCID": "PIDF_Soldier_AssaultRifle",
    "Level": 30,
    "X": 230,
    "Y": -486,
    "Z": 4097
}
```
