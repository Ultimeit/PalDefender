### Schema der 200-Antwort

| Feld | Typ | Beschreibung |
|---|---|---|
| `Banlist` | object | Sperrlistendaten nach Anwendung der Abfragefilter. |

Schema des `Banlist`-Objekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Version` | integer | Dateiformatversion der Sperrliste. |
| `BannedMessage` | string | Nachricht, die gesperrten Spielern angezeigt wird. |
| `UserEntries` | object[] | Benutzersperren, die den angegebenen Filtern entsprechen. |
| `IPEntries` | object[] | IP-Sperren, die den angegebenen Filtern entsprechen. |

Schema eines `UserEntries[]`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `UserId` | string | Gesperrte Benutzer-ID. |
| `Active` | boolean | Gibt an, ob die Sperre derzeit aktiv ist. |
| `BannedBy` | object | Ausstellerdaten der Sperraktion. |
| `UnbannedBy` | object | Ausstellerdaten der Entsperraktion, falls vorhanden. |

Schema eines `IPEntries[]`-Eintrags:

| Feld | Typ | Beschreibung |
|---|---|---|
| `IP` | string | Gesperrte IP-Adresse. |
| `Active` | boolean | Gibt an, ob die Sperre derzeit aktiv ist. |
| `BannedBy` | object | Ausstellerdaten der Sperraktion. |
| `UnbannedBy` | object | Ausstellerdaten der Entsperraktion, falls vorhanden. |

Schema des Ausstellerobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `Type` | string | Ausstellertyp, etwa `rest`, `player` oder `system`. |
| `NameValue` | string | Name, Benutzer-ID, Token oder ersatzweise Typ des Ausstellers. |
| `IP` | string | Metadaten zur IP-Adresse des Ausstellers. |
| `Reason` | string | Für die Aktion gespeicherter Grund. |
| `Timestamp` | object | UTC-Zeitstempelkomponenten der Aktion. |

Schema des Zeitstempelobjekts:

| Feld | Typ | Beschreibung |
|---|---|---|
| `UTC` | integer | Unix-Zeitstempel in Sekunden. |
| `Year` | integer | UTC-Jahr. |
| `Month` | integer | UTC-Monat. |
| `Day` | integer | UTC-Tag des Monats. |
| `Hour` | integer | UTC-Stunde. |
| `Min` | integer | UTC-Minute. |
| `Sec` | integer | UTC-Sekunde. |
| `Msec` | integer | Millisekundenkomponente. |
