# 📄 `PalSummon.json`

Eine PalSummon-Datei definiert eine Begegnung an einem festen Ort, die mit `/summon <Dateiname>` gestartet wird. Speichere die Dateien unter `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/` und referenzierte PalTemplates unter `Pals/Templates/`.

!!! tip "ID-Suche"
    Nutze [paldeck.cc/pals](https://paldeck.cc/pals) für `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) für Passives und [paldeck.cc/skills](https://paldeck.cc/skills) für Skill-IDs des referenzierten Templates.

## Begegnungsschlüssel

| Schlüssel | Typ | Standard | Beschreibung |
| --- | --- | --- | --- |
| `PalTemplate` | string | Erforderlich | Dateiname eines Templates in `Pals/Templates/`; `.json` kann weggelassen werden. |
| `BossBattleName` | string | Pal-ID | Anzeigename in Ankündigungen, Logs, Webhooks und Schadensergebnissen. |
| `Uncapturable` | bool | `false` | Verhindert dauerhaft, dass der beschworene Pal gefangen werden kann. |
| `CapturableAtHealthPercent` | number | `15` | Macht den Pal ab diesem HP-Prozentsatz oder darunter fangbar (`0`–`100`). Wird bei `Uncapturable: true` ignoriert. |
| `DisableAI` | bool | `false` | Deaktiviert die normale KI. Einzelne passive Verhaltensweisen wie Ausweichen können weiterhin auftreten. |
| `DisableDamageMeter` | bool | `false` | Deaktiviert Tracking, Ergebnisdialog und Rangbelohnungen. Stattdessen wird die `Default`-Belohnung an alle Online-Spieler vergeben. |
| `SpawnScale` | number | `1.0` | Visueller/physischer Größenmultiplikator; Werte kleiner oder gleich null fallen auf `1.0` zurück. |
| `HealthMultiplier` | number | `1.0` | Multiplikator der maximalen Lebenspunkte; muss endlich und größer als null sein. |
| `DamageTakenMultiplier` | number | `1.0` | Multiplikator für erhaltenen Schaden; negative Werte fallen auf `1.0` zurück. |
| `DamageDealtMultiplier` | number | `1.0` | Multiplikator für verursachten Schaden; negative Werte fallen auf `1.0` zurück. |
| `X`, `Y`, `Z` | number | Erforderlich | Kartenkoordinaten. Ermittle sie mit `/getpos`. |
| `DisableStatuses` | array | Leer | Zu unterdrückende Statusnamen. Ungültige Namen werden übersprungen. |
| `Rewards` | object | Leer | Optionale rangspezifische und standardmäßige [Belohnungsdefinitionen](#schadensmesser-und-belohnungen). |

`CapturableAt`, `CapturableAtPercent` und `capturable_at` werden als Kompatibilitätsalias akzeptiert. `HPMultiplier`, `AdditionalEnemyMaxHPRate`, `AdditionalEnemyReceiveDamageRate` und `AdditionalEnemyInflictDamageRate` werden ebenfalls akzeptiert, die Namen aus der Tabelle werden jedoch empfohlen.

## Schadensmesser und Belohnungen

Der Ergebnisdialog zeigt die fünf Spieler mit dem höchsten Schaden, hebt die ersten drei hervor und zeigt immer die eigene Position des Empfängers. Ein Belohnungsobjekt kann feste `Drops` und zufällige `Pools` enthalten.

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

Numerische Schlüssel sind Positionen des Schadensmessers. `Default` gilt für Positionen ohne eigene Rangbelohnung. Wenn `DisableDamageMeter` auf `true` steht, wird nur `Default` verwendet und jeder Online-Spieler erhält diese Belohnung.

Für einfache Fortschrittsbelohnungen können `EXP`, `TechnologyPoints` oder `AncientTechnologyPoints` auch direkt in einem Rang-/Default-Objekt stehen; `Drops` ist sinnvoll, wenn sie mit Gegenständen und Eiern kombiniert werden.

### Belohnungseinträge

Jeder Eintrag muss genau einen Belohnungstyp definieren:

| Belohnung | Pflichtfelder | Optionale Felder |
| --- | --- | --- |
| Gegenstand | `ItemID` | `Count` (Standard `1`) |
| Pal-Ei | `EggID`, `PalTemplate` | `Count` (Standard `1`), `Level` (Template-Level bei `0`) |
| Erfahrung | `EXP` | — |
| Technologiepunkte | `TechnologyPoints` | — |
| Antike Technologiepunkte | `AncientTechnologyPoints` | — |

Mengen können als feste Ganzzahl oder `{ "Min": 1, "Max": 3 }` angegeben werden. Direkte `Drops` dürfen eine `Chance` von `0` bis `100` enthalten. Pool-Einträge nutzen `Weight` in gewichteten Modi, `Chance` bei `Independent` und können `Unique` überschreiben.

### Loot-Pools

| Pool-Schlüssel | Standard | Beschreibung |
| --- | --- | --- |
| `Name` | Leer | Optionale Bezeichnung für Diagnosemeldungen. |
| `Mode` | `OneOf` | `OneOf`, `Pick`, `All` oder `Independent`. |
| `Chance` | `100` | Wahrscheinlichkeit, dass der gesamte Pool aktiviert wird. |
| `Rolls` | `1` | Anzahl der Auswahlen bei `Pick`. |
| `Unique` | `true` | Verhindert doppelte Auswahlen bei `Pick`; ein Eintrag kann dies überschreiben. |
| `Entries` | Erforderlich | Array der Belohnungseinträge. |

- `OneOf` wählt anhand von `Weight` einen Eintrag aus.
- `Pick` führt `Rolls` gewichtete Auswahlen durch.
- `All` vergibt jeden Eintrag.
- `Independent` würfelt die `Chance` jedes Eintrags separat.

```json
"Pools": [
    {
        "Name": "Rare drop",
        "Mode": "OneOf",
        "Chance": 25,
        "Entries": [
            { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 4 },
            { "EggID": "PalEgg_Dragon_05", "PalTemplate": "RaidReward.json", "Level": 50, "Weight": 1 }
        ]
    }
]
```

## Vollständiges Beispiel

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Arena Anubis",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "HealthMultiplier": 8.0,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "Winner bonus",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## Validierungscheckliste

1. Teste das referenzierte Template zuerst mit `/givemepal_j <Template>`.
2. Ermittle `X`, `Y` und `Z` mit `/getpos`; bei RCON muss `/getpos` eine UserId erhalten.
3. Verwende gültiges JSON ohne Kommentare oder nachgestellte Kommas.
4. Verwende pro Belohnungszeile nur einen Belohnungstyp.
6. Führe `/summon <Dateiname>` aus und prüfe das PalDefender-Log auf genaue Validierungsfehler.
