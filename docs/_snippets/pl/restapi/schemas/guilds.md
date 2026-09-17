### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Meta` | obiekt | Metadane listy gildii. |
| `Guilds` | obiekt | Podsumowania znanych gildii według UUID gildii. |

`Meta` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `GuildCount` | liczba całkowita | Liczba zwróconych gildii. |

Podsumowanie gildii — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `name` | ciąg znaków | Nazwa gildii. |
| `Level` | liczba całkowita | Poziom obozu bazowego gildii. |
| `admin` | obiekt | Dane administratora gildii. |
| `camp_count` | liczba całkowita | Liczba obozów bazowych gildii. |
| `camps` | tablica obiektów | Podsumowania obozów bazowych. |
| `member_count` | liczba całkowita | Liczba członków gildii. |
| `members` | tablica ciągów znaków | Wartości PlayerUID członków gildii. |

`admin` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `id` | ciąg znaków | PlayerUID administratora. |
| `name` | ciąg znaków | Nazwa gracza będącego administratorem. |

`camps[]` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `id` | ciąg znaków | GUID obozu bazowego. |
| `world_pos` | obiekt | Współrzędne obozu bazowego w świecie. |
| `map_pos` | obiekt | Przeliczone współrzędne mapy. |

Współrzędne — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `x` | liczba | Współrzędna X. |
| `y` | liczba | Współrzędna Y. |
| `z` | liczba | Współrzędna Z. |
