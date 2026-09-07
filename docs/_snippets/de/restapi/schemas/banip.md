### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Success` | boolean | `true`, wenn die IP-Sperre gespeichert wurde. |
| `IP` | string | Gesperrte IP-Adresse. |
| `UserId` | string | Optional mit der IP-Sperre gespeicherte Benutzer-ID. |
| `Kicked` | integer | Anzahl der Online-Spieler, die von dieser IP-Adresse vom Server entfernt wurden. |
