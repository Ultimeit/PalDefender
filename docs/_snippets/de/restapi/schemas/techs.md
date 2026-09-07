### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Meta` | object | Metadaten zur Technologieanzahl des Zielspielers. |
| `Techs` | object | Technologiedaten des Zielspielers. |

Schema des `Meta`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `PlayerUID` | string | Von den Palworld-Speicherdaten verwendete Spieler-UID. |
| `Player` | string | In der Anfrage-URL angegebene Spielerkennung. |
| `UnlockedCount` | integer | Anzahl der derzeit freigeschalteten Technologien. |
| `LockedCount` | integer | Anzahl der derzeit gesperrten Technologien. |
| `TotalCount` | integer | Gesamtzahl der in den Spielerdaten bekannten Rezepttechnologien. |

Schema des `Techs`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Unlocked` | string[] | Derzeit vom Spieler erlernte Technologie-IDs. |
