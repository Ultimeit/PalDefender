### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Granted` | object | Durch die Anfrage gewährte Fortschrittswerte. |
| `Totals` | object | Aktualisierte Summen gewährter Währungen, sofern zutreffend. |

Schema des `Granted`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `EXP` | integer | Gewährte EXP, sofern angefordert. |
| `Relics` | object | Nach Relikttyp gewährte Reliktpunkte, sofern angefordert. |
| `TechnologyPoints` | integer | Gewährte Technologiepunkte, sofern angefordert. |
| `AncientTechnologyPoints` | integer | Gewährte antike Technologiepunkte, sofern angefordert. |

Schema des `Totals`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Relics` | object | Aktualisierte Reliktpunktsummen nach Typ, wenn `Relics` gewährt wurde. |
| `TechnologyPoints` | integer | Aktualisierte Gesamtzahl der Technologiepunkte, wenn `TechnologyPoints` gewährt wurde. |
| `AncientTechnologyPoints` | integer | Aktualisierte Gesamtzahl der antiken Technologiepunkte, wenn `AncientTechnologyPoints` gewährt wurde. |
