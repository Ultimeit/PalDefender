### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Meta` | obiekt | Metadane wskazanego gracza. |
| `Inventory` | obiekt | Pojemniki ekwipunku wskazanego gracza. |

`Meta` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `PlayerUID` | ciąg znaków | UID gracza używany w danych zapisu Palworld. |
| `Player` | ciąg znaków | Identyfikator gracza podany w ścieżce żądania. |

`Inventory` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Items` | obiekt | Pojemnik zwykłego ekwipunku. |
| `KeyItems` | obiekt | Pojemnik przedmiotów kluczowych. |
| `Weapons` | obiekt | Pojemnik wyposażonej broni. |
| `Armor` | obiekt | Pojemnik pancerza. |
| `Food` | obiekt | Pojemnik jedzenia. |
| `DropSlot` | obiekt | Pojemnik miejsca upuszczania. |

Pojemnik ekwipunku — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Available` | wartość logiczna | Czy pojemnik był dostępny. |
| `ContainerID` | ciąg znaków | Identyfikator pojemnika Palworld lub pusty ciąg znaków, jeśli jest niedostępny. |
| `UsedSlots` | liczba całkowita | Liczba zajętych miejsc. |
| `MaxSlots` | liczba całkowita | Łączna liczba miejsc. |
| `FreeSlots` | liczba całkowita | Liczba wolnych miejsc. |
| `Slots` | obiekt | Zajęte miejsca według indeksu miejsca. |

`Slots` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `ItemID` | ciąg znaków | Identyfikator przedmiotu Palworld. |
| `Count` | liczba całkowita | Liczba sztuk w stosie w miejscu. |
