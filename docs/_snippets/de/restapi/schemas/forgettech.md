### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `ForgottenCount` | integer | Anzahl der vom Spieler entfernten Technologien. |
| `Forgotten` | string[] oder string | Entfernte Technologie-IDs oder `All`, wenn alle freigeschalteten Technologien entfernt wurden. |
| `Skipped` | string[] | Übersprungene Technologie-IDs, weil sie nicht freigeschaltet waren. |
