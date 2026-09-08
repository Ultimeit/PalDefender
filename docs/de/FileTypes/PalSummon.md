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
| `Rewards` | object oder array | Leer | Optionale rangspezifische und standardmäßige [Belohnungsdefinitionen](#damage-meter-and-rewards). Die Objektform wird empfohlen. |

`CapturableAt`, `CapturableAtPercent` und `capturable_at` werden als Kompatibilitätsalias akzeptiert. `HPMultiplier`, `AdditionalEnemyMaxHPRate`, `AdditionalEnemyReceiveDamageRate` und `AdditionalEnemyInflictDamageRate` werden ebenfalls akzeptiert, die Namen aus der Tabelle werden jedoch empfohlen.

## Schadensanzeige und Belohnungen { #damage-meter-and-rewards }

Belohnungen werden ermittelt, nachdem der beschworene Pal gestorben ist oder gefangen wurde. Die Schadensrangliste ist vom höchsten zum niedrigsten Schaden sortiert. Der Ergebnisdialog zeigt die ersten fünf Plätze, hebt die ersten drei hervor und zeigt zusätzlich die eigene Position des jeweiligen Spielers, wenn sie außerhalb der ersten fünf liegt.

Bei aktivierter Schadensverfolgung wird jeder teilnehmende Spieler wie folgt behandelt:

1. PalDefender sucht nach einem numerischen `Rewards`-Schlüssel, der dem endgültigen Rang dieses Spielers entspricht.
2. Wenn dieser genaue Rang nicht existiert, verwendet PalDefender `Rewards.Default`.
3. Wenn beides nicht existiert, erhält dieser Spieler keine Belohnung.
4. Die ausgewählte Belohnung wird für diesen Spieler separat ausgewürfelt. Zwei Spieler, die dieselbe `Default`-Definition verwenden, können daher unterschiedliche Zufallsergebnisse erhalten.

Nur Teilnehmer, die am Ende der Begegnung noch online sind und über einen verfügbaren Player-Controller verfügen, können Rangbelohnungen erhalten. Eine nummerierte Belohnung wird nicht mit `Default` kombiniert, sondern ersetzt `Default` für diesen Rang.

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

In diesem Beispiel erhält der Erstplatzierte beide garantierten Drops, der Zweitplatzierte erhält einen zufälligen Betrag von EXP und jeder andere Teilnehmer auf der Rangliste hat unabhängig eine 75-prozentige Chance, 1.000 Money zu erhalten.

Rangschlüssel müssen positive ganze Zahlen sein, die als JSON-Objektschlüssel geschrieben werden, z. B. `"1"`, `"2"` oder `"10"`. `"0"`, negative Ränge und beliebige Namen sind ungültig. `Default` wird ohne Berücksichtigung der Groß-/Kleinschreibung abgeglichen.

??? note "Array-Form"
    `Rewards` kann auch ein Array sein. Array-Element 0 hat Rang 1, Element 1 hat Rang 2 und so weiter. Die Array-Form kann `Default` nicht definieren, daher ist die Objektform klarer und wird empfohlen.

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### Struktur der Belohnungsdefinition

Jeder Rang und `Default` enthält eine Belohnungsdefinition. Eine Definition kann beides enthalten:

- `Drops`: Einträge werden direkt und unabhängig ausgewertet.
- `Pools`: Gruppen, die steuern, wie Einträge ausgewählt werden.

Es kann auch die Progressionskürzel `EXP`, `TechnologyPoints` und `AncientTechnologyPoints` enthalten. Abkürzungen sind garantiert und nützlich, wenn sie keine eigene Einstellung `Chance`, `Weight` oder `Unique` benötigen.

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### Arten von Belohnungseinträgen

Jeder Eintrag muss genau eine Belohnungsart definieren. Kombinieren Sie kein Element, ein Ei und ein Fortschrittsfeld im selben Eintrag.

| Belohnung | Erforderliche Felder | Optionale Felder | Notizen |
| --- | --- | --- | --- |
| Gegenstand | `ItemID` | `Count`, `Chance`, `Weight`, `Unique` | `Count` ist standardmäßig `1`. |
| Pal-Ei | `EggID`, `PalTemplate` | `Count`, `Level`, `Chance`, `Weight`, `Unique` | `Count` ist standardmäßig `1`; `Level: 0` verwendet das Level des Templates. |
| Erfahrung | `EXP` | `Chance`, `Weight`, `Unique` | Der `EXP`-Wert ist der Betrag oder Bereich. |
| Technologiepunkte | `TechnologyPoints` | `Chance`, `Weight`, `Unique` | Der Feldwert ist der Betrag oder Bereich. |
| Antike Technologiepunkte | `AncientTechnologyPoints` | `Chance`, `Weight`, `Unique` | Der Feldwert ist der Betrag oder Bereich. |

`Chance`, `Weight` und `Unique` sind nur in den unten beschriebenen Kontexten wirksam. Wenn ein Feld vom Parser akzeptiert wird, bedeutet das nicht, dass es sich auf alle Verteilungsmodi auswirkt.

Die oben genannten kanonischen Feldnamen werden empfohlen. Der Parser akzeptiert auch diese Aliase:

| Kanonisches Feld | Akzeptierte Aliase |
| --- | --- |
| `ItemID` | `ItemId`, `ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`, `Num` |
| `EXP` | `Exp`, `Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### Feste Werte, Bereiche und Chancen

Beträge können eine feste ganze Zahl oder ein inklusiver Bereich sein:

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- `Count`, EXP und Technologiepunktbeträge müssen ganze Zahlen von mindestens `1` sein.
- Ein Bereich benötigt sowohl `Min` als auch `Max` und `Max` darf nicht niedriger als `Min` sein.
- Textbereiche wie `"1-3"` sind ungültig; Verwenden Sie `{ "Min": 1, "Max": 3 }`.
- Ei `Level` kann `0` sein; Dadurch wird die Ebene vom referenzierten PalTemplate beibehalten. Ein positiver Level überschreibt den Template-Level und ist auf Level 255 begrenzt, wenn das Ei gewährt wird.
- `Chance` akzeptiert eine Zahl oder einen numerischen Text mit einem optionalen `%`, zum Beispiel `30`, `30.5` oder `"30%"`.
- `Chance: 0` ist nie erfolgreich, `Chance: 100` ist immer erfolgreich und die Werte müssen zwischen `0` und `100` bleiben.
- Für eine Chance, die streng zwischen 0 und 100 liegt, muss der generierte Wurf niedriger sein als der konfigurierte Wert. Ein Wurf von genau `30.0` scheitert daher an einem `Chance` von `30`.

### Direkte Drops

Jeder Eintrag in `Drops` wird unabhängig ausgewertet. Es gibt keine Auswahl-Eins-Beziehung zwischen benachbarten Einträgen. Das Fehlen von `Chance` bedeutet `100`.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

Der Money ist garantiert. Die Munition, EXP und Technologiepunkte machen jeweils ihren eigenen Zufallswurf. Es können null, ein, zwei oder alle drei optionalen Drops erfolgreich sein.

`Weight` und `Unique` funktionieren nicht im direkten `Drops` und erzeugen Warnungen. Verwenden Sie `Chance` für optionale direkte Drops.

## Beutepools

Ein Pool prüft zuerst seine eigene `Chance`. Schlägt diese Prüfung fehl, wird keiner seiner Einträge berücksichtigt. Bei Erfolg bestimmt `Mode`, wie die Einträge ausgewertet werden.

| Poolschlüssel | Geben Sie | ein Standard | Beschreibung |
| --- | --- | --- | --- |
| `Name` | Zeichenfolge | Leer | Optionales Diagnoseetikett. Es hat keinen Einfluss auf die Auswahl. |
| `Mode` | Zeichenfolge | `OneOf` | `OneOf`, `Pick`, `All` oder `Independent`. Beim Matching wird die Groß-/Kleinschreibung nicht beachtet. |
| `Chance` | Zahlen- oder Prozenttext | `100` | Chance, dass der gesamte Pool aktiviert wird. |
| `Rolls` | ganze Zahl | `1` | Anzahl der Auswahlen in `Pick`; von den anderen Modi ignoriert. |
| `Unique` | bool | `true` | Standard-Wiederholungsrichtlinie für `Pick`; ein Eintrag kann ihn überschreiben. |
| `Entries` | Array | Erforderlich | Nicht leere Liste von Belohnungseinträgen. |

`One` wird als Alias für `OneOf` und `PickN` als Alias für `Pick` akzeptiert, es werden jedoch die kanonischen Modusnamen empfohlen.

| Modus | Wie viele Einträge können gewährt werden? | Verwendet `Weight`? | Verwendet Eintrag `Chance`? | Verwendet `Rolls` / `Unique`? |
| --- | --- | --- | --- | --- |
| `OneOf` | Genau eins, wenn der Pool erfolgreich ist | Ja | Nein | Nein |
| `Pick` | Bis zu `Rolls` Auswahlmöglichkeiten | Ja | Nein | Ja |
| `All` | Jeder Eintrag einmal, wenn der Pool erfolgreich ist | Nein | Nein | Nein |
| `Independent` | Null durch alle Einträge | Nein | Ja | Nein |

All Vier Modi verwenden weiterhin die Poolebene `Chance`. Mehrere Pools in einer Belohnungsdefinition werden unabhängig voneinander verarbeitet und ihre Ergebnisse werden dem direkten `Drops` hinzugefügt.

### `OneOf`: ein gewichtetes Ergebnis

`OneOf` ist der Standardmodus. Wenn die Chance auf Poolebene erfolgreich ist, wird genau ein Eintrag ausgewählt. Die Wahrscheinlichkeit eines Eintrags ist sein `Weight` geteilt durch die Summe aller Eintragsgewichte.

```json
{
    "Pools": [
        {
            "Name": "Equipment jackpot",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

Die Gewichtungen betragen insgesamt 20. Abhängig vom Erfolg des Pools haben die vier Einträge Wahrscheinlichkeiten von 35 %, 35 %, 25 % und 5 %. Da der Pool selbst nur in 35 % der Fälle aktiviert wird, beträgt die absolute Chance des Eies `35% × 5% = 1.75%`.

- Fehlt `Weight`, wird standardmäßig `1` verwendet.
- `Weight` muss eine ganze Zahl von mindestens `1` sein; Entfernen Sie einen Eintrag, anstatt das Gewicht `0` zuzuweisen.
- `Rolls` wird ignoriert und erzeugt eine Warnung, da `OneOf` immer einmal auswählt.
- Der Eintrag `Chance` wird ignoriert und erzeugt eine Warnung. Verwenden Sie `Weight`, um die relative Auswahlwahrscheinlichkeit zu steuern.
- `Unique` hat keine praktische Auswirkung, da nur ein Eintrag ausgewählt ist.

### `Pick`: mehrfach gewichtete Ergebnisse ohne Wiederholungen

`Pick` wiederholt die gewichtete Auswahl `Rolls` Mal. Mit der Standardeinstellung `Unique: true` wird ein ausgewählter Eintrag vor der nächsten Auswahl entfernt und kann nicht erneut ausgewählt werden. Die Gewichtungen werden nach jeder Auswahl aus den verbleibenden Einträgen neu berechnet.

```json
{
    "Pools": [
        {
            "Name": "Choose two different rewards",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

Dadurch werden zwei unterschiedliche Einträge gewährt. Wenn `Rolls` größer als die Anzahl der verfügbaren eindeutigen Einträge ist, wird die Auswahl beendet, wenn keine Einträge mehr vorhanden sind. es ist kein Fehler.

### `Pick`: wiederholte Ergebnisse zulassen

Setzen Sie den `Unique` des Pools auf `false`, um ausgewählte Einträge für spätere Rolls verfügbar zu halten. Wiederholte Zuteilungen desselben Artikels werden vor der Lieferung zusammengeführt.

```json
{
    "Pools": [
        {
            "Name": "Three supply rolls",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

All Drei Würfe können Money auswählen, alle können Munition auswählen oder die Ergebnisse können gemischt sein. Wenn Sie beispielsweise Money zweimal auswählen, entsteht ein Money-Zuschuss von 10.000 statt zwei separater Zuschüsse.

### `Pick`: Überschreibt `Unique` pro Eintrag

Ein `Unique` der Eintragsebene überschreibt die Pool-Standardeinstellung nur für diesen Eintrag. Dies ermöglicht wiederholbare gemeinsame Belohnungen und einmalige Jackpot-Belohnungen im selben Pool.

```json
{
    "Pools": [
        {
            "Name": "Repeatable currency with unique jackpots",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

Money bleibt nach der Auswahl in der Kandidatenliste, da der Eintrag `Unique: false` lautet. Die Rüstung und der Helm erben `Unique: true` aus dem Pool und werden nach der Auswahl entfernt. Das Umgekehrte gilt auch: Ein Pool kann `Unique: false` verwenden, während ein bestimmter Eintrag `Unique: true` verwendet.

### `All`: jeden Eintrag gewähren

`All` gewährt jeden Eintrag genau einmal, wenn der Pool-Level `Chance` erfolgreich ist.

```json
{
    "Pools": [
        {
            "Name": "Complete reward bundle",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`Weight`, die Einstiegsversion `Chance` und `Unique` haben keinen Einfluss auf `All`. `Rolls` wird ignoriert und erzeugt eine Warnung. Um das gesamte Bundle optional zu machen, legen Sie den `Chance` des Pools fest. Um einzelne Einträge optional zu machen, verwenden Sie stattdessen `Independent` oder direkt `Drops`.

### `Independent`: Jeden Eintrag einzeln würfeln

`Independent` prüft jeden Eintrag und verwendet den eigenen `Chance` jedes Eintrags. Es können keine Einträge, ein Eintrag, mehrere Einträge oder alle Einträge gewährt werden.

```json
{
    "Pools": [
        {
            "Name": "Independent bonus rolls",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

Erstens besteht eine Chance von 80 %, dass der Pool aktiviert wird. Wenn es aktiviert wird, ist Money garantiert, da sein Eintrag `Chance` weglässt; Die anderen drei Einträge würfeln unabhängig voneinander mit 50 %, 10 % und 5 %.

- Fehlender Eintrag `Chance` ist standardmäßig `100`.
- `Weight` und `Unique` haben keinen Einfluss auf diesen Modus.
- `Rolls` wird ignoriert und erzeugt eine Warnung, da jeder Eintrag einmal überprüft wird.

### Kombination von direkten Drops und mehreren Pools

Verwenden Sie mehrere Pools, wenn ein Empfänger mehrere unabhängig strukturierte Belohnungsebenen erhalten soll.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "One equipment item",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "Two supply rolls",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "Rare independent bonuses",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

Es gelten immer die direkten Money und EXP. Der erste Pool fügt einen Ausrüstungsgegenstand hinzu, der zweite trifft zwei gewichtete Versorgungsauswahlen mit Ersatz und der dritte führt zwei unabhängige Bonuswürfe durch. Ein Spieler kann Ergebnisse aus jedem Pool erhalten, da die Pools nicht miteinander konkurrieren.

### Pal-Ei-Belohnungen

Ein Ei benötigt sowohl `EggID` als auch `PalTemplate`. Die Vorlage wird aus `Pals/Templates/` geladen und `.json` kann weggelassen werden. `Count` steuert, wie viele Eier gewährt werden. `Level: 0` oder eine weggelassene Ebene behält die Vorlagenebene bei; ein positiver fester Wert oder Bereich überschreibt ihn.

```json
{
    "Pools": [
        {
            "Name": "One random egg reward",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

Wenn eine Ei-Vorlage bei Gewährung der Belohnung nicht importiert werden kann, protokolliert PalDefender einen Fehler und überspringt die Ei-Belohnung.

### Wiederholte Ergebnisse zusammenführen

Ergebnisse aus direkten Drops und allen Pools werden vor der Lieferung kombiniert:

- Elemente mit demselben `ItemID` werden durch Addition ihrer Anzahl zusammengeführt.
- Eier verschmelzen nur, wenn `EggID`, `PalTemplate` und der gewürfelte `Level` alle identisch sind.
- EXP, Technologiepunkte und antike Technologiepunkte werden addiert.
- Die Summe der zu gewährenden Artikel und Technologiepunkte wird auf das vorzeichenbehaftete 32-Bit-Maximum (`2,147,483,647`) beschränkt.

Das bedeutet, dass wiederholte `Pick`-Ergebnisse keine doppelten Inventarzeilen in der Belohnungsanfrage erzeugen. Eier mit unterschiedlich ausgewürfelten Leveln bleiben separate Belohnungen.

### `DisableDamageMeter`-Verteilung

Wenn `DisableDamageMeter` auf `true` steht, erstellt PalDefender keine Schadensrangliste und verwendet keine nummerierten Rangbelohnungen. Stattdessen wird `Rewards.Default` separat für **jeden Spieler ausgewürfelt, der am Ende der Begegnung online ist** – auch für Spieler, die dem beschworenen Pal keinen Schaden zugefügt haben.

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

Der Money wird jedem Online-Spieler gewährt. Jeder Spieler würfelt unabhängig voneinander die beiden optionalen Punktbelohnungen. Wenn `Default` fehlt oder leer ist, erhält in diesem Modus niemand eine Belohnung und PalDefender schreibt eine Warnung in das Protokoll.

### Ungültige und ignorierte Kombinationen

Ungültige Belohnungsdaten verhindern das Laden der Datei PalSummon. Unbekannte oder kontextuell ignorierte Felder erzeugen Warnungen, sodass Rechtschreibfehler und unwirksame Einstellungen im PalDefender-Protokoll sichtbar sind.

| Konfiguration | Ergebnis |
| --- | --- |
| Ein Eintrag enthält sowohl `ItemID` als auch `EXP` | Fehler: Ein Eintrag darf nur einen Belohnungstyp definieren. |
| Ein Belohnungseintrag hat kein Gegenstands-, Ei- oder Fortschrittsfeld | Fehler: PalDefender weiß nicht, was gewährt werden soll. |
| `Count: 0`, `Weight: 0` oder `Rolls: 0` | Fehler: Diese Werte müssen mindestens `1` sein. |
| Ein Bereich lässt `Min` oder `Max` weg oder hat `Max < Min` | Fehler. |
| `Chance` liegt außerhalb von `0`–`100` | Fehler. |
| Ein Pool hat kein `Entries`, ein leeres `Entries`-Array oder einen Nicht-Array-Wert | Fehler. |
| `Chance` wird auf einem `OneOf`-, `Pick`- oder `All`-Eintrag platziert | Warnung; Die Eintrittschance wird ignoriert. |
| `Rolls` ist auf `OneOf`, `All` oder `Independent` | festgelegt Warnung; `Rolls` wird ignoriert. |
| `Weight` oder `Unique` wird direkt in `Drops` | platziert Warnung; Verwenden Sie `Chance` für direkte Drops. |
| Ein unbekanntes Feld wie `Wieght` ist vorhanden | Warnung; Das Feld ist unbenutzt. |

Verwenden Sie einen gültigen JSON ohne Kommentare oder nachgestellte Kommas. Überprüfen Sie Ladewarnungen, auch wenn die Beschwörung noch geladen wird: Warnungen weisen normalerweise auf eine Einstellung hin, die keine Auswirkung hat.

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
4. Verwende pro Belohnungseintrag nur einen Belohnungstyp.
5. Prüfe, dass jeder Pool ein nicht leeres `Entries`-Array besitzt und nur Felder verwendet, die im gewählten `Mode` wirksam sind.
6. Führe `/summon <Dateiname>` aus und prüfe das PalDefender-Log auf genaue Validierungsfehler und Warnungen.
