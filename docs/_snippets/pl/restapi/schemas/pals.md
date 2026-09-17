### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Meta` | obiekt | Metadane wskazanego gracza i liczby Pali. |
| `Pals` | obiekt | Pale wskazanego gracza w drużynie, Palboxie i obozach bazowych. |

`Meta` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `PlayerUID` | ciąg znaków | UID gracza używany w danych zapisu Palworld. |
| `Player` | ciąg znaków | Identyfikator gracza podany w ścieżce żądania. |
| `TeamCount` | liczba całkowita | Liczba Pali w drużynie gracza. |
| `PalboxCount` | liczba całkowita | Liczba Pali w Palboxie gracza. |
| `BaseCampCount` | liczba całkowita | Liczba uwzględnionych obozów bazowych. |

`Pals` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Team` | obiekt | Pale drużyny według identyfikatora instancji Pala. |
| `Palbox` | obiekt | Pale Palboxa według identyfikatora instancji Pala. |
| `BaseCamps` | tablica obiektów | Obozy bazowe gildii i przypisane do nich pracujące Pale. |

Pal — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `PalID` | ciąg znaków | Identyfikator gatunku Pala. |
| `UniqueNPCID` | ciąg znaków | Unikalny identyfikator NPC, jeśli jest dostępny. |
| `Nickname` | ciąg znaków | Niestandardowy pseudonim Pala lub pusty ciąg znaków. |
| `SkinId` | ciąg znaków | Identyfikator skórki lub pusty ciąg znaków. |
| `Gender` | ciąg znaków | Płeć Pala. |
| `Level` | liczba całkowita | Poziom Pala. |
| `Exp` | liczba całkowita | EXP Pala. |
| `Shiny` | wartość logiczna | Czy jest to rzadki Pal. |
| `PartnerSkillLevel` | liczba całkowita | Ranga umiejętności partnerskiej. |
| `CondensedPals` | liczba całkowita | Postęp rangi kondensacji. |
| `UnusedStatusPoints` | liczba całkowita | Niewydane punkty atrybutów Pala. |
| `FriendshipPoints` | liczba całkowita | Liczba punktów przyjaźni. |
| `PhysicalHealth` | ciąg znaków | Stan zdrowia fizycznego. |
| `WorkerSick` | ciąg znaków | Stan choroby pracownika. |
| `ImportedCharacter` | wartość logiczna | Czy oznaczono jako zaimportowany. |
| `HP` | liczba | Bieżące HP. |
| `MP` | liczba | Bieżące MP, jeśli jest dostępne. |
| `SP` | liczba | Bieżąca wytrzymałość, jeśli jest dostępna. |
| `Shield` | liczba | Bieżąca wartość osłony, jeśli jest dostępna. |
| `Hunger` | liczba | Bieżąca wartość głodu. |
| `MaxHunger` | liczba | Maksymalna wartość głodu. |
| `SAN` | liczba | Wartość poczytalności. |
| `Support` | liczba całkowita | Wartość wsparcia. |
| `CraftSpeed` | liczba całkowita | Wartość szybkości wytwarzania. |
| `PalSouls` | obiekt | Rangi ulepszeń duszami Pala: `Health`, `Attack`, `Defense` i `CraftSpeed`. |
| `IVs` | obiekt | Wartości IV: `Health`, `AttackMelee`, `AttackShot` i `Defense`. |
| `ActiveSkills` | tablica ciągów znaków | Wyposażone umiejętności aktywne. |
| `LearntSkills` | tablica ciągów znaków | Poznane umiejętności. |
| `Passives` | tablica ciągów znaków | Identyfikatory umiejętności pasywnych. |
| `ExtraWorkSuitabilities` | obiekt | Dodatkowe rangi predyspozycji do pracy według identyfikatora predyspozycji. |
| `DisableWorkPreferences` | tablica ciągów znaków | Identyfikatory wyłączonych preferencji pracy. |
| `team_slot_index` | liczba całkowita | Indeks miejsca w drużynie, tylko dla Pali `Team`. |
| `page` | liczba całkowita | Indeks strony Palboxa, tylko dla Pali `Palbox`. |
| `slot` | liczba całkowita | Indeks miejsca w Palboxie, tylko dla Pali `Palbox`. |
| `base_camp_slot_index` | liczba całkowita | Indeks miejsca pracownika obozu bazowego, tylko dla Pali obozu bazowego. |

`BaseCamps[]` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `id` | ciąg znaków | GUID obozu bazowego. |
| `level` | liczba całkowita | Poziom obozu bazowego. |
| `world_pos` | obiekt | Współrzędne obozu bazowego w świecie. |
| `map_pos` | obiekt | Przeliczone współrzędne mapy. |
| `state` | ciąg znaków | Bieżący stan obozu bazowego. |
| `pals` | obiekt | Pale pracujące w obozie bazowym według identyfikatora instancji Pala. |

Współrzędne — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `x` | liczba | Współrzędna X. |
| `y` | liczba | Współrzędna Y. |
| `z` | liczba | Współrzędna Z. |
