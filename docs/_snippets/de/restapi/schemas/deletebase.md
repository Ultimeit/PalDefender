### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `BaseCamp` | object | Zusammenfassung des gelöschten Basislagers. |
| `Deleted` | object | Bereinigungszahlen der gelöschten Basislagerdaten. |
| `Archive` | string | Pfad zum erstellten Prüfarchiv. |

Schema des `BaseCamp`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Id` | string | GUID des Basislagers. |
| `Summary` | string | Lesbare Zusammenfassung des Basislagers. |

Schema des `Deleted`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `BaseCampPals` | integer | Anzahl der gelöschten Basislager-Pals. |
| `StorageContainers` | integer | Anzahl der geleerten Lagercontainer. |
| `ItemStacks` | integer | Anzahl der gelöschten Gegenstandsstapel. |
| `ItemCount` | integer | Gesamtzahl der gelöschten Gegenstände. |
| `Buildings` | integer | Anzahl der gelöschten Gebäude. |
| `DropItems` | integer | Anzahl der gelöschten fallengelassenen Gegenstandsakteure. |
| `DefenseModels` | integer | Anzahl der gelöschten Verteidigungsmodelle. |
| `OtherMapObjects` | integer | Anzahl der gelöschten sonstigen Kartenobjekte. |
| `PalBox` | boolean | Gibt an, ob die Palbox der Basis gelöscht wurde. |
