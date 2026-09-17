### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Meta` | obiekt | Metadane liczby technologii wskazanego gracza. |
| `Techs` | obiekt | Dane technologii wskazanego gracza. |

`Meta` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `PlayerUID` | ciąg znaków | UID gracza używany w danych zapisu Palworld. |
| `Player` | ciąg znaków | Identyfikator gracza podany w ścieżce żądania. |
| `UnlockedCount` | liczba całkowita | Liczba obecnie odblokowanych technologii. |
| `LockedCount` | liczba całkowita | Liczba obecnie zablokowanych technologii. |
| `TotalCount` | liczba całkowita | Łączna liczba technologii receptur znanych w danych gracza. |

`Techs` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Unlocked` | tablica ciągów znaków | Identyfikatory technologii obecnie poznanych przez gracza. |
