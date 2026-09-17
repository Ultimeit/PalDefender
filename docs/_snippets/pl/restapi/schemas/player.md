### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Player` | obiekt | Szczegóły gracza. |

`Player` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Name` | ciąg znaków | Bieżąca lub zapisana nazwa gracza. |
| `IP` | ciąg znaków | Adres IP gracza lub pusty ciąg znaków, jeśli jest niedostępny. |
| `PlayerUID` | ciąg znaków | UID gracza używany w danych zapisu Palworld. |
| `UserId` | ciąg znaków | Identyfikator użytkownika platformy lub pusty ciąg znaków, jeśli jest niedostępny. |
| `GuildName` | ciąg znaków | Nazwa gildii lub pusty ciąg znaków, jeśli jest niedostępna. |
| `GuildUUID` | ciąg znaków | UUID gildii lub zerowy GUID, jeśli jest niedostępny. |
| `Status` | ciąg znaków | Zapisany stan konta gracza. |
| `WorldLocation` | obiekt | Bieżące lub ostatnio zapisane współrzędne w świecie. |
| `MapLocation` | obiekt | Przeliczone współrzędne mapy. |

Pozycja — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `x` | liczba | Współrzędna X. |
| `y` | liczba | Współrzędna Y. |
| `z` | liczba | Współrzędna Z. |
