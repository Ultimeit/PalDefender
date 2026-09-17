### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `BaseCamp` | obiekt | Podsumowanie usuniętego obozu bazowego. |
| `Deleted` | obiekt | Liczby usuniętych elementów danych obozu bazowego. |
| `Archive` | ciąg znaków | Ścieżka do wygenerowanego archiwum kontroli. |

`BaseCamp` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Id` | ciąg znaków | GUID obozu bazowego. |
| `Summary` | ciąg znaków | Czytelne podsumowanie obozu bazowego. |

`Deleted` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `BaseCampPals` | liczba całkowita | Liczba usuniętych Pali obozu bazowego. |
| `StorageContainers` | liczba całkowita | Liczba opróżnionych pojemników magazynowych. |
| `ItemStacks` | liczba całkowita | Liczba usuniętych stosów przedmiotów. |
| `ItemCount` | liczba całkowita | Łączna liczba usuniętych sztuk przedmiotów. |
| `Buildings` | liczba całkowita | Liczba usuniętych budowli. |
| `DropItems` | liczba całkowita | Liczba usuniętych obiektów wyrzuconych przedmiotów. |
| `DefenseModels` | liczba całkowita | Liczba usuniętych modeli obronnych. |
| `OtherMapObjects` | liczba całkowita | Liczba usuniętych pozostałych obiektów mapy. |
| `PalBox` | wartość logiczna | Czy usunięto Palbox bazy. |
