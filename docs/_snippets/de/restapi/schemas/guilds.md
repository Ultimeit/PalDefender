### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Meta` | object | Metadaten der Gildenliste. |
| `Guilds` | object | Bekannte Gildenzusammenfassungen, nach Gilden-UUID indiziert. |

Schema des `Meta`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `GuildCount` | integer | Anzahl der zurückgegebenen Gilden. |

Schema einer Gildenzusammenfassung:

| Feld | Typ | Beschreibung |
|---|---|---|
| `name` | string | Gildenname. |
| `Level` | integer | Basislagerstufe der Gilde. |
| `admin` | object | Details zum Gildenadministrator. |
| `camp_count` | integer | Anzahl der Basislager der Gilde. |
| `camps` | object[] | Zusammenfassungen der Basislager. |
| `member_count` | integer | Anzahl der Gildenmitglieder. |
| `members` | string[] | PlayerUID-Werte der Gildenmitglieder. |

Schema des `admin`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `id` | string | PlayerUID des Administrators. |
| `name` | string | Spielername des Administrators. |

Schema eines `camps[]`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `id` | string | GUID des Basislagers. |
| `world_pos` | object | Weltkoordinaten des Basislagers. |
| `map_pos` | object | Umgerechnete Kartenkoordinaten. |

Schema des Koordinatenobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `x` | number | X-Koordinate. |
| `y` | number | Y-Koordinate. |
| `z` | number | Z-Koordinate. |
