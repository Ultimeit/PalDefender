### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Player` | object | Spielerdetails. |

Schema des `Player`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Name` | string | Aktueller oder gespeicherter Spielername. |
| `IP` | string | IP-Adresse des Spielers oder eine leere Zeichenfolge, wenn nicht verfügbar. |
| `PlayerUID` | string | Von den Palworld-Speicherdaten verwendete Spieler-UID. |
| `UserId` | string | Plattform-Benutzer-ID oder eine leere Zeichenfolge, wenn nicht verfügbar. |
| `GuildName` | string | Gildenname oder eine leere Zeichenfolge, wenn nicht verfügbar. |
| `GuildUUID` | string | Gilden-UUID oder eine Null-GUID, wenn nicht verfügbar. |
| `Status` | string | Gespeicherter Status des Spielerkontos. |
| `WorldLocation` | object | Aktuelle oder zuletzt gespeicherte Weltkoordinaten. |
| `MapLocation` | object | Umgerechnete Kartenkoordinaten. |

Schema des Positionsobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `x` | number | X-Koordinate. |
| `y` | number | Y-Koordinate. |
| `z` | number | Z-Koordinate. |
