### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Meta` | obiekt | Metadane wskazanego gracza. |
| `Progression` | obiekt | Dane postępów, walut, pokonanych przeciwników, schwytań i aktywności. |

`Meta` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `PlayerUID` | ciąg znaków | UID gracza używany w danych zapisu Palworld. |
| `Player` | ciąg znaków | Identyfikator gracza podany w ścieżce żądania. |

`Progression` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Player` | obiekt | Poziom gracza, EXP i niewydane punkty atrybutów. |
| `Currencies` | obiekt | Sumy punktów reliktów i technologii. |
| `Bosses` | obiekt | Liczniki i flagi pokonania bossów. |
| `Captures` | obiekt | Liczniki schwytań i rozbioru Pali. |
| `Activities` | obiekt | Liczniki wytwarzania, lochów, wędkarstwa, skarbów i innych aktywności. |

`Progression.Player` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `level` | liczba całkowita | Bieżący poziom gracza. |
| `exp` | liczba całkowita | Bieżąca wartość EXP. |
| `unusedStatusPoints` | liczba całkowita | Niewydane punkty atrybutów gracza. |

`Progression.Currencies` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `relics` | obiekt | Sumy punktów reliktów według typu reliktu. |
| `technologyPoints` | liczba całkowita | Suma punktów technologii. |
| `ancientTechnologyPoints` | liczba całkowita | Suma punktów starożytnej technologii. |

`Progression.Bosses` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `towerBossDefeatCounts` | obiekt | Liczby pokonań bossów wież według identyfikatora bossa. |
| `normalBossDefeatFlags` | obiekt | Flagi pokonania zwykłych bossów według identyfikatora bossa. |
| `raidBossDefeatCounts` | obiekt | Liczby pokonań bossów rajdowych według identyfikatora bossa. |
| `totalBossDefeatCount` | liczba całkowita | Suma pokonań bossów wież. |
| `predatorDefeatCount` | liczba całkowita | Liczba pokonanych drapieżników. |

`Progression.Captures` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `tribeCaptureCount` | liczba całkowita | Łączna liczba schwytań plemienia. |
| `palCaptureCounts` | obiekt | Liczby schwytań Pali według identyfikatora Pala. |
| `palCaptureBonusCounts` | obiekt | Liczniki premii za schwytanie według identyfikatora Pala. |
| `palButcherCounts` | obiekt | Liczby rozbiorów Pali według identyfikatora Pala. |

`Progression.Activities` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `craftItemCounts` | obiekt | Liczby wytworzonych przedmiotów według identyfikatora przedmiotu. |
| `normalDungeonClearCount` | liczba całkowita | Liczba ukończonych zwykłych lochów. |
| `fixedDungeonClearCount` | liczba całkowita | Liczba ukończonych stałych lochów. |
| `oilrigClearCount` | liczba całkowita | Liczba ukończonych platform wiertniczych. |
| `palRankUpCounts` | obiekt | Liczby awansów rang Pali według identyfikatora Pala. |
| `arenaSoloClearCounts` | obiekt | Liczby ukończeń areny solo według identyfikatora areny. |
| `npcTalkCounts` | obiekt | Liczby rozmów z NPC według identyfikatora NPC. |
| `fishingCounts` | obiekt | Liczby połowów według identyfikatora ryby. |
| `foundTreasureCount` | liczba całkowita | Liczba znalezionych skarbów. |
| `campConqueredCount` | liczba całkowita | Liczba zdobytych obozów. |
| `firstFishingComplete` | wartość logiczna | Czy zapisano ukończenie pierwszego połowu. |
