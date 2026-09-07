### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Guild` | object | Gildendetails. |

Schema des `Guild`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `name` | string | Gildenname. |
| `Level` | integer | Basislagerstufe der Gilde. |
| `admin` | object | Details zum Gildenadministrator. |
| `member_count` | integer | Anzahl der Gildenmitglieder. |
| `members` | object[] | Detaillierte Datensätze der Gildenmitglieder. |
| `camp_count` | integer | Anzahl der Basislager der Gilde. |
| `camps` | object[] | Detaillierte Datensätze der Basislager. |
| `items` | object | Daten des Gilden-Gegenstandslagers. |
| `expeditions` | object | Expeditionsdaten der Gilde. |
| `laboratory` | object | Forschungsdaten des Gildenlabors. |

Schema des `admin`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `id` | string | PlayerUID des Administrators. |
| `name` | string | Spielername des Administrators. |

Schema eines `members[]`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `player_uid` | string | PlayerUID des Mitglieds. |
| `player_name` | string | Spielername des Mitglieds. |
| `status` | string | Status des Mitglieds. |

Schema eines `camps[]`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `id` | string | GUID des Basislagers. |
| `level` | integer | Stufe des Basislagers. |
| `world_pos` | object | Weltkoordinaten des Basislagers. |
| `map_pos` | object | Umgerechnete Kartenkoordinaten. |
| `state` | string | Aktueller Zustand des Basislagers. |
| `pals` | object | Arbeiter-Pals des Basislagers, nach Pal-Instanz-ID indiziert. |
| `buildings` | string | Platzhalter für die aktuelle Gebäudenutzlast. |

Schema des Koordinatenobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `x` | number | X-Koordinate. |
| `y` | number | Y-Koordinate. |
| `z` | number | Z-Koordinate. |

Schema eines Basislager-Pal-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `nickname` | string | Spitzname des Pals. |
| `pal_id` | string | Artkennung des Pals. |
| `npc_id` | string | Eindeutige NPC-ID. |
| `skin_id` | string | Skin-ID. |
| `gender` | string | Geschlecht des Pals. |
| `level` | integer | Stufe des Pals. |
| `shiny` | boolean | Gibt an, ob dies ein seltener Pal ist. |
| `phisical_health` | string | Von der aktuellen API zurückgegebener körperlicher Gesundheitszustand. |
| `worker_sick` | string | Krankheitszustand des Arbeiters. |
| `san` | number | Verstandswert. |
| `imported` | boolean | Gibt an, ob der Pal als importiert markiert ist. |
| `friendship` | integer | Freundschaftspunktwert. |
| `active_skills` | string[] | Ausgerüstete aktive Skills. |
| `learnt_skills` | string[] | Erlernte Skills. |
| `passives` | string[] | Passive Skill-IDs. |

Schema des `items`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `container_id` | string | ID des Gilden-Gegenstandscontainers, sofern verfügbar. |
| `current` | integer | Anzahl der belegten Plätze. |
| `max` | integer | Gesamtzahl der Plätze. |
| `<slot_index>` | object | Nach numerischem Platzindex indiziertes Gegenstandsobjekt. |

Schema eines Gilden-Gegenstandsplatzes:

| Feld | Typ | Beschreibung |
|---|---|---|
| `item_id` | string | Gegenstands-ID auf dem Platz. |
| `count` | integer | Stapelanzahl auf dem Platz. |

Schema des `expeditions`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `finished` | integer | Anzahl abgeschlossener Expeditionen. |
| `missions` | object | Freigabemarker der Missionen, nach Missions-ID indiziert. |

Schema des `laboratory`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `current_research` | string | Aktuelle Forschungs-ID. |
| `researches` | object | Aktiver Forschungsfortschritt, nach Forschungs-ID indiziert. |

Schema eines Forschungsfortschrittsobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `work_amount` | number | Aktueller Arbeitswert. |
| `required_work_amount` | number | Erforderlicher Arbeitswert. |
| `percentage` | number | Aktueller Arbeitswert geteilt durch den erforderlichen Arbeitswert. |
