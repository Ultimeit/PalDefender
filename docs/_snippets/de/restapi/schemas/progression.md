### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Meta` | object | Metadaten des Zielspielers. |
| `Progression` | object | Fortschritts-, Währungs-, Besiegungs-, Fang- und Aktivitätsdaten. |

Schema des `Meta`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `PlayerUID` | string | Von den Palworld-Speicherdaten verwendete Spieler-UID. |
| `Player` | string | In der Anfrage-URL angegebene Spielerkennung. |

Schema des `Progression`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Player` | object | Spielerstufe, EXP und ungenutzte Statuspunkte. |
| `Currencies` | object | Summen von Relikt- und Technologiepunkten. |
| `Bosses` | object | Zähler und Marker besiegter Bosse. |
| `Captures` | object | Zähler gefangener und geschlachteter Pals. |
| `Activities` | object | Zähler für Herstellung, Dungeons, Angeln, Schätze und andere Aktivitäten. |

Schema des `Progression.Player`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `level` | integer | Aktuelle Spielerstufe. |
| `exp` | integer | Aktueller EXP-Wert. |
| `unusedStatusPoints` | integer | Ungenutzte Statuspunkte des Spielers. |

Schema des `Progression.Currencies`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `relics` | object | Reliktpunktsummen, nach Relikttyp indiziert. |
| `technologyPoints` | integer | Gesamtzahl der Technologiepunkte. |
| `ancientTechnologyPoints` | integer | Gesamtzahl der antiken Technologiepunkte. |

Schema des `Progression.Bosses`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `towerBossDefeatCounts` | object | Besiegungszahlen der Turmbosse, nach Boss-ID indiziert. |
| `normalBossDefeatFlags` | object | Besiegungsmarker normaler Bosse, nach Boss-ID indiziert. |
| `raidBossDefeatCounts` | object | Besiegungszahlen der Raidbosse, nach Boss-ID indiziert. |
| `totalBossDefeatCount` | integer | Summe der Besiegungszahlen von Turmbossen. |
| `predatorDefeatCount` | integer | Anzahl besiegter Raubtiere. |

Schema des `Progression.Captures`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `tribeCaptureCount` | integer | Gesamtzahl der Stammesfänge. |
| `palCaptureCounts` | object | Pal-Fangzahlen, nach Pal-ID indiziert. |
| `palCaptureBonusCounts` | object | Pal-Fangbonuszahlen, nach Pal-ID indiziert. |
| `palButcherCounts` | object | Schlachtzahlen von Pals, nach Pal-ID indiziert. |

Schema des `Progression.Activities`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `craftItemCounts` | object | Hergestellte Gegenstandsmengen, nach Gegenstands-ID indiziert. |
| `normalDungeonClearCount` | integer | Anzahl abgeschlossener normaler Dungeons. |
| `fixedDungeonClearCount` | integer | Anzahl abgeschlossener fester Dungeons. |
| `oilrigClearCount` | integer | Anzahl abgeschlossener Oil Rigs. |
| `palRankUpCounts` | object | Rangaufstiege von Pals, nach Pal-ID indiziert. |
| `arenaSoloClearCounts` | object | Solo-Abschlüsse von Arenen, nach Arena-ID indiziert. |
| `npcTalkCounts` | object | NPC-Gesprächszahlen, nach NPC-ID indiziert. |
| `fishingCounts` | object | Fangzahlen beim Angeln, nach Fisch-ID indiziert. |
| `foundTreasureCount` | integer | Anzahl gefundener Schätze. |
| `campConqueredCount` | integer | Anzahl eroberter Lager. |
| `firstFishingComplete` | boolean | Gibt an, ob der erste Angelabschluss gespeichert ist. |
