### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Guild` | obiekt | Szczegóły gildii. |

`Guild` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `name` | ciąg znaków | Nazwa gildii. |
| `Level` | liczba całkowita | Poziom obozu bazowego gildii. |
| `admin` | obiekt | Dane administratora gildii. |
| `member_count` | liczba całkowita | Liczba członków gildii. |
| `members` | tablica obiektów | Szczegółowe wpisy członków gildii. |
| `camp_count` | liczba całkowita | Liczba obozów bazowych gildii. |
| `camps` | tablica obiektów | Szczegółowe wpisy obozów bazowych. |
| `items` | obiekt | Dane magazynu przedmiotów gildii. |
| `expeditions` | obiekt | Dane ekspedycji gildii. |
| `laboratory` | obiekt | Dane badań laboratoryjnych gildii. |

`admin` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `id` | ciąg znaków | PlayerUID administratora. |
| `name` | ciąg znaków | Nazwa gracza będącego administratorem. |

`members[]` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `player_uid` | ciąg znaków | PlayerUID członka. |
| `player_name` | ciąg znaków | Nazwa gracza będącego członkiem. |
| `status` | ciąg znaków | Status członka. |

`camps[]` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `id` | ciąg znaków | GUID obozu bazowego. |
| `level` | liczba całkowita | Poziom obozu bazowego. |
| `world_pos` | obiekt | Współrzędne obozu bazowego w świecie. |
| `map_pos` | obiekt | Przeliczone współrzędne mapy. |
| `state` | ciąg znaków | Bieżący stan obozu bazowego. |
| `pals` | obiekt | Pale pracujące w obozie bazowym według identyfikatora instancji Pala. |
| `buildings` | ciąg znaków | Obecny element zastępczy danych budowli. |

Współrzędne — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `x` | liczba | Współrzędna X. |
| `y` | liczba | Współrzędna Y. |
| `z` | liczba | Współrzędna Z. |

Pal obozu — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `nickname` | ciąg znaków | Pseudonim Pala. |
| `pal_id` | ciąg znaków | Identyfikator gatunku Pala. |
| `npc_id` | ciąg znaków | Unikalny identyfikator NPC. |
| `skin_id` | ciąg znaków | Identyfikator skórki. |
| `gender` | ciąg znaków | Płeć Pala. |
| `level` | liczba całkowita | Poziom Pala. |
| `shiny` | wartość logiczna | Czy jest to rzadki Pal. |
| `phisical_health` | ciąg znaków | Stan zdrowia fizycznego zwracany przez aktualne API. |
| `worker_sick` | ciąg znaków | Stan choroby pracownika. |
| `san` | liczba | Wartość poczytalności. |
| `imported` | wartość logiczna | Czy oznaczono jako zaimportowany. |
| `friendship` | liczba całkowita | Liczba punktów przyjaźni. |
| `active_skills` | tablica ciągów znaków | Wyposażone umiejętności aktywne. |
| `learnt_skills` | tablica ciągów znaków | Poznane umiejętności. |
| `passives` | tablica ciągów znaków | Identyfikatory umiejętności pasywnych. |

`items` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `container_id` | ciąg znaków | Identyfikator pojemnika przedmiotów gildii, jeśli jest dostępny. |
| `current` | liczba całkowita | Liczba zajętych miejsc. |
| `max` | liczba całkowita | Łączna liczba miejsc. |
| `<slot_index>` | obiekt | Obiekt przedmiotów według liczbowego indeksu miejsca. |

Miejsce przedmiotu gildii — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `item_id` | ciąg znaków | Identyfikator przedmiotu w miejscu. |
| `count` | liczba całkowita | Liczba sztuk w stosie w miejscu. |

`expeditions` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `finished` | liczba całkowita | Liczba zakończonych ekspedycji. |
| `missions` | obiekt | Flagi udostępnionych misji według identyfikatora misji. |

`laboratory` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `current_research` | ciąg znaków | Identyfikator bieżącego badania. |
| `researches` | obiekt | Postępy aktywnych badań według identyfikatora badania. |

Postęp badań — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `work_amount` | liczba | Bieżąca ilość wykonanej pracy. |
| `required_work_amount` | liczba | Wymagana ilość pracy. |
| `percentage` | liczba | Bieżąca ilość pracy podzielona przez wymaganą. |
