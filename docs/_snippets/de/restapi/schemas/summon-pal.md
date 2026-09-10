### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Summoned` | object | Details des erzeugten Pals. |

`Summoned` enthält `Type` (`"Pal"`), `PalID`, `Level`, `Uncapturable`, `DisableAI`, `DamageMeter` sowie die angeforderten Werte `X`, `Y` und `Z`. Wurde ein Template verwendet, wird außerdem `PalTemplate` zurückgegeben.
