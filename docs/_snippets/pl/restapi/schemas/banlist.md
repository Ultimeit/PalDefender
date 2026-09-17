### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Banlist` | obiekt | Dane listy blokad po zastosowaniu filtrów zapytania. |

`Banlist` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Version` | liczba całkowita | Wersja formatu pliku listy blokad. |
| `BannedMessage` | ciąg znaków | Komunikat wyświetlany zablokowanym graczom. |
| `UserEntries` | tablica obiektów | Wpisy blokad użytkowników zgodne z podanymi filtrami. |
| `IPEntries` | tablica obiektów | Wpisy blokad IP zgodne z podanymi filtrami. |

`UserEntries[]` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `UserId` | ciąg znaków | Identyfikator zablokowanego użytkownika. |
| `Active` | wartość logiczna | Czy blokada jest obecnie aktywna. |
| `BannedBy` | obiekt | Dane wystawcy blokady. |
| `UnbannedBy` | obiekt | Dane osoby lub systemu cofającego blokadę, jeśli są dostępne. |

`IPEntries[]` — schemat elementu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `IP` | ciąg znaków | Zablokowany adres IP. |
| `Active` | wartość logiczna | Czy blokada jest obecnie aktywna. |
| `BannedBy` | obiekt | Dane wystawcy blokady. |
| `UnbannedBy` | obiekt | Dane osoby lub systemu cofającego blokadę, jeśli są dostępne. |

Wystawca — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Type` | ciąg znaków | Typ wystawcy, na przykład `rest`, `player` lub `system`. |
| `NameValue` | ciąg znaków | Nazwa wystawcy, identyfikator użytkownika, token lub zastępczo nazwa typu. |
| `IP` | ciąg znaków | Metadane adresu IP wystawcy. |
| `Reason` | ciąg znaków | Powód zapisany dla działania. |
| `Timestamp` | obiekt | Składowe znacznika czasu UTC działania. |

Znacznik czasu — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `UTC` | liczba całkowita | Znacznik czasu Unix w sekundach. |
| `Year` | liczba całkowita | Rok UTC. |
| `Month` | liczba całkowita | Miesiąc UTC. |
| `Day` | liczba całkowita | Dzień miesiąca UTC. |
| `Hour` | liczba całkowita | Godzina UTC. |
| `Min` | liczba całkowita | Minuta UTC. |
| `Sec` | liczba całkowita | Sekunda UTC. |
| `Msec` | liczba całkowita | Składowa milisekund. |
