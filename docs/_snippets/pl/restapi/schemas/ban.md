### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Success` | wartość logiczna | `true`, gdy blokada została zapisana. |
| `UserId` | ciąg znaków | Identyfikator zablokowanego użytkownika. |
| `IP` | wartość logiczna | Czy żądanie zablokowało również adres IP. |
| `BannedIP` | ciąg znaków | Zablokowany adres IP lub pusty ciąg znaków, jeśli nie zablokowano IP. |
| `Kicked` | liczba całkowita | Liczba graczy online wyrzuconych w wyniku blokady. |
