### Schemat odpowiedzi 200

| Pole | Typ | Opis |
|-------|------|-------------|
| `Granted` | obiekt | Wartości postępów przyznane przez żądanie. |
| `Totals` | obiekt | Zaktualizowane sumy przyznanych walut, jeśli dotyczy. |

`Granted` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `EXP` | liczba całkowita | Przyznane EXP, jeśli zażądano ich przyznania. |
| `Relics` | obiekt | Przyznane punkty reliktów według typu, jeśli zażądano ich przyznania. |
| `TechnologyPoints` | liczba całkowita | Przyznane punkty technologii, jeśli zażądano ich przyznania. |
| `AncientTechnologyPoints` | liczba całkowita | Przyznane punkty starożytnej technologii, jeśli zażądano ich przyznania. |

`Totals` — schemat obiektu:

| Pole | Typ | Opis |
|-------|------|-------------|
| `Relics` | obiekt | Zaktualizowane sumy punktów reliktów według typu, jeśli przyznano `Relics`. |
| `TechnologyPoints` | liczba całkowita | Zaktualizowana suma punktów technologii, jeśli przyznano `TechnologyPoints`. |
| `AncientTechnologyPoints` | liczba całkowita | Zaktualizowana suma punktów starożytnej technologii, jeśli przyznano `AncientTechnologyPoints`. |
