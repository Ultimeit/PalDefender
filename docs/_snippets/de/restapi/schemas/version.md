### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Version` | object | Details zur PalDefender-Version. |

Schema des `Version`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Major` | integer | Hauptversionsnummer. |
| `Minor` | integer | Nebenversionsnummer. |
| `Patch` | integer | Patch-Versionsnummer. |
| `Build` | integer | Buildnummer. |
| `Version` | string | Kurze Versionszeichenfolge. |
| `VersionLong` | string | Lange Versionszeichenfolge. |
| `Beta` | boolean | Gibt an, ob dieser Build als Beta gekennzeichnet ist. |
