### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Meta` | object | Metadaten des Zielspielers. |
| `Inventory` | object | Inventarcontainer des Zielspielers. |

Schema des `Meta`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `PlayerUID` | string | Von den Palworld-Speicherdaten verwendete Spieler-UID. |
| `Player` | string | In der Anfrage-URL angegebene Spielerkennung. |

Schema des `Inventory`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Items` | object | Allgemeiner Inventarcontainer. |
| `KeyItems` | object | Inventarcontainer für Schlüsselgegenstände. |
| `Weapons` | object | Inventarcontainer der Waffenausrüstung. |
| `Armor` | object | Rüstungsinventarcontainer. |
| `Food` | object | Nahrungsinventarcontainer. |
| `DropSlot` | object | Inventarcontainer des Ablageplatzes. |

Schema eines Inventarcontainers:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Available` | boolean | Gibt an, ob der Container verfügbar war. |
| `ContainerID` | string | Palworld-Container-ID oder eine leere Zeichenfolge, wenn nicht verfügbar. |
| `UsedSlots` | integer | Anzahl der belegten Plätze. |
| `MaxSlots` | integer | Gesamtzahl der Plätze. |
| `FreeSlots` | integer | Anzahl der freien Plätze. |
| `Slots` | object | Belegte Plätze, nach Platzindex indiziert. |

Schema eines `Slots`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `ItemID` | string | Palworld-Gegenstandskennung. |
| `Count` | integer | Stapelanzahl auf dem Platz. |
