### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Meta` | object | Metadaten des Zielspielers und Pal-Anzahlen. |
| `Pals` | object | Team-, Palbox- und Basislager-Pals des Zielspielers. |

Schema des `Meta`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `PlayerUID` | string | Von den Palworld-Speicherdaten verwendete Spieler-UID. |
| `Player` | string | In der Anfrage-URL angegebene Spielerkennung. |
| `TeamCount` | integer | Anzahl der Pals im Spielerteam. |
| `PalboxCount` | integer | Anzahl der Pals in der Palbox des Spielers. |
| `BaseCampCount` | integer | Anzahl der enthaltenen Basislager. |

Schema des `Pals`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Team` | object | Team-Pals, nach Pal-Instanz-ID indiziert. |
| `Palbox` | object | Palbox-Pals, nach Pal-Instanz-ID indiziert. |
| `BaseCamps` | object[] | Gildenbasislager und deren zugewiesene Arbeiter-Pals. |

Schema eines Pal-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `PalID` | string | Artkennung des Pals. |
| `UniqueNPCID` | string | Eindeutige NPC-ID, falls vorhanden. |
| `Nickname` | string | Eigener Pal-Spitzname oder eine leere Zeichenfolge. |
| `SkinId` | string | Skin-ID oder eine leere Zeichenfolge. |
| `Gender` | string | Geschlecht des Pals. |
| `Level` | integer | Stufe des Pals. |
| `Exp` | integer | EXP des Pals. |
| `Shiny` | boolean | Gibt an, ob dies ein seltener Pal ist. |
| `PartnerSkillLevel` | integer | Rang der Partnerfähigkeit. |
| `CondensedPals` | integer | Fortschritt des Kondensierungsrangs. |
| `UnusedStatusPoints` | integer | Ungenutzte Statuspunkte des Pals. |
| `FriendshipPoints` | integer | Freundschaftspunktwert. |
| `PhysicalHealth` | string | Körperlicher Gesundheitszustand. |
| `WorkerSick` | string | Krankheitszustand des Arbeiters. |
| `ImportedCharacter` | boolean | Gibt an, ob der Pal als importiert markiert ist. |
| `HP` | number | Aktuelle HP. |
| `MP` | number | Aktuelle MP, falls vorhanden. |
| `SP` | number | Aktuelle Ausdauer, falls vorhanden. |
| `Shield` | number | Aktueller Schildwert, falls vorhanden. |
| `Hunger` | number | Aktueller Hungerwert. |
| `MaxHunger` | number | Maximaler Hungerwert. |
| `SAN` | number | Verstandswert. |
| `Support` | integer | Unterstützungswert. |
| `CraftSpeed` | integer | Herstellungsgeschwindigkeit. |
| `PalSouls` | object | Pal-Seelenränge mit `Health`, `Attack`, `Defense` und `CraftSpeed`. |
| `IVs` | object | IV-Werte mit `Health`, `AttackMelee`, `AttackShot` und `Defense`. |
| `ActiveSkills` | string[] | Ausgerüstete aktive Skills. |
| `LearntSkills` | string[] | Erlernte Skills. |
| `Passives` | string[] | Passive Skill-IDs. |
| `ExtraWorkSuitabilities` | object | Zusätzliche Arbeitseignungsränge, nach Eignungs-ID indiziert. |
| `DisableWorkPreferences` | string[] | Deaktivierte Arbeitseinstellungs-IDs. |
| `team_slot_index` | integer | Teamplatzindex, nur bei Pals unter `Team`. |
| `page` | integer | Palbox-Seitenindex, nur bei Pals unter `Palbox`. |
| `slot` | integer | Palbox-Platzindex, nur bei Pals unter `Palbox`. |
| `base_camp_slot_index` | integer | Arbeiterplatzindex des Basislagers, nur bei Basislager-Pals. |

Schema eines `BaseCamps[]`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `id` | string | GUID des Basislagers. |
| `level` | integer | Stufe des Basislagers. |
| `world_pos` | object | Weltkoordinaten des Basislagers. |
| `map_pos` | object | Umgerechnete Kartenkoordinaten. |
| `state` | string | Aktueller Zustand des Basislagers. |
| `pals` | object | Arbeiter-Pals des Basislagers, nach Pal-Instanz-ID indiziert. |

Schema des Koordinatenobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `x` | number | X-Koordinate. |
| `y` | number | Y-Koordinate. |
| `z` | number | Z-Koordinate. |
