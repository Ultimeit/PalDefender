### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Success` | boolean | `true`, wenn die Sperre gespeichert wurde. |
| `UserId` | string | Gesperrte Benutzer-ID. |
| `IP` | boolean | Gibt an, ob die Anfrage auch eine IP-Adresse gesperrt hat. |
| `BannedIP` | string | Gesperrte IP-Adresse oder eine leere Zeichenfolge, wenn keine IP gesperrt wurde. |
| `Kicked` | integer | Anzahl der durch die Sperre vom Server entfernten Online-Spieler. |
