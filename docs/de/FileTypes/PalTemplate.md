# :octicons-file-16: `PalTemplate.json`

Mit <https://paldeck.cc/creator> kannst du diese Dateien deutlich einfacher erstellen.

!!! tip "ID-Suche"
    Nutze [paldeck.cc/pals](https://paldeck.cc/pals) für `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) für `Passives` und [paldeck.cc/skills](https://paldeck.cc/skills) für `ActiveSkills` und `LearntSkills`.

| Schlüssel                      | Typ   | Beschreibung                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | string | Interne ID des Pals, der erzeugt werden soll. Gültige [`PalID`](https://paldeck.cc/pals)-Werte findest du auf Paldeck. |
| `UniqueNPCID`            | string | Interne ID des Pals, der als NPC erzeugt werden soll. |
| `Nickname`               | string | Optionaler Spitzname für den Pal. |
| `SkinId`                 | string | Skin-Override für den Pal (für benutzerdefinierte Optik). Nutze `/getskinids`, um IDs abzurufen. |
| `Gender`                 | string | `"Male"`, `"Female"` oder `"None"`. |
| `Level`                  | int    | Das Level des Pals.                                                               |
| `Exp`                    | int    | Erfahrungspunkte. |
| `Shiny`                  | bool   | Gibt an, ob der Pal shiny ist. |
| `PartnerSkillLevel`      | int    | Level der Partnerfähigkeit des Pals. Darf nicht kleiner als 1 sein! |
| `CondensedPals`          | int    | Anzahl der Pals, die in diesen Pal verdichtet wurden. |
| `UnusedStatusPoints`     | int    | Verfügbare Statuspunkte zur manuellen Verteilung. Vermutlich nur für Spieler relevant. |
| `FriendshipPoints`       | int    | Freundschaftswert des Pals. |
| `PhysicalHealth`         | string | Körperlicher Gesundheitszustand. Gültige Namen sind unter anderem `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick`             | string | Krankheitszustand des Arbeiters. Gültige Namen sind unter anderem `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter`      | bool   | Markiert den Pal als importierten Charakter. |
| `HP` / `SP` / `MP`       | number | Basiswerte für Gesundheit, Ausdauer und Mana. |
| `Shield`                 | number | Schildwert. |
| `Hunger` / `MaxHunger`   | int    | Aktueller und maximaler Hungerwert. |
| `SAN`                    | int    | Sanity-Wert, also die mentale Stabilität des Pals. |
| `Support`                | int    | Support-Level, das für KI-Verhalten und Skills verwendet wird. |
| `CraftSpeed`             | int    | Multiplikator für Handwerksgeschwindigkeit. |
| `PalSouls`               | object | Passive Soul-Boni. Enthält `Health`, `Attack`, `Defense`, `CraftSpeed`. Empfohlene Normalwerte werden über deine Importregeln gesteuert. |
| `IVs`                    | object | Individuelle Statuswerte. Enthält `Health`, `AttackMelee`, `AttackShot`, `Defense`. Empfohlene Normalwerte werden über deine Importregeln gesteuert. |
| `ActiveSkills`           | array  | Liste der aktuell ausgerüsteten Skills (max. 3). Wenn mehr als 3 Einträge angegeben werden, gelten die zusätzlichen Einträge als gelernte Skills. Gültige [Skill-IDs](https://paldeck.cc/skills) findest du auf Paldeck. |
| `LearntSkills`           | array  | Skills, die der Pal gelernt hat und einwechseln kann. Aktive Skills sollten hier nicht stehen. Gültige [Skill-IDs](https://paldeck.cc/skills) findest du auf Paldeck. |
| `Passives`               | array  | Passive Eigenschaften des Pals. Normale Pals sollten höchstens 4 Passives verwenden. Gültige [`PassiveID`](https://paldeck.cc/passives)-Werte findest du auf Paldeck. |
| `ExtraWorkSuitabilities` | object | Verstärkte Arbeitstypen und Level (z. B. `"Mining": 2`). Verfügbare Arbeitstypen: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |
| `DisableWorkPreferences` | array  | Arbeitstypen, die der Pal verweigert. Verfügbare Arbeitstypen: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Anleitung

1. Erstelle pro benutzerdefiniertem Pal eine JSON-Datei in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Nutze einen eindeutigen Dateinamen, zum Beispiel `RaidRewardAnubis.json`. Befehle können meist `RaidRewardAnubis` oder `RaidRewardAnubis.json` verwenden.
3. `PalID` muss immer vorhanden sein. Alles andere ist optional; fehlende Werte verwenden die Standardwerte von PalDefender oder Palworld.
4. `Level` und `PartnerSkillLevel` müssen jeweils `1` oder höher sein.
5. Trage nur die 3 ausgerüsteten Angriffe in `ActiveSkills` ein. Zusätzliche bekannte Angriffe gehören in `LearntSkills`.
6. Nutze exakte IDs für Pals, Skills, Passives, Skins und Arbeitstypen. Falsche IDs können den Import fehlschlagen lassen oder ignoriert werden.
7. Validiere JSON vor dem Hochladen. JSON erlaubt keine Kommentare oder nachgestellten Kommas.
8. Wenn ein Template importiert wird, Werte aber geändert oder blockiert werden, prüfe `Pals/ImportRules/Default.json` und alle Pal-spezifischen Überschreibungen auf dem Server.

## Einrichtungsschritte

1. Lege fest, wofür das Template gedacht ist: einfache Admin-Belohnung, Eventboss, Test-Pal oder Spawn-Template für eine Summon-Datei.
2. Wähle die `PalID` auf [paldeck.cc/pals](https://paldeck.cc/pals). Der Anzeigename ist nicht immer die Datei-ID, kopiere die ID daher exakt.
3. Füge nur die Felder hinzu, die du wirklich steuern willst. Ein kurzes Template ist leichter zu debuggen als ein sehr großes.
4. Wähle Skills auf [paldeck.cc/skills](https://paldeck.cc/skills). Die drei ausgerüsteten Angriffe gehören in `ActiveSkills`; zusätzliche bekannte Angriffe in `LearntSkills`.
5. Wähle Passives auf [paldeck.cc/passives](https://paldeck.cc/passives). Für normale Nutzung sollten es höchstens vier Passives sein, außer dein Server erlaubt bewusst mehr.
6. Speichere die Datei in `Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
7. Teste zuerst mit `/givemepal_j <filename>`. Danach kannst du dasselbe Template für `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, die REST API oder `PalSummon.json` verwenden.

## Erklärung der Beispiele

Das Minimalbeispiel unten erstellt einen Anubis auf Level 50 mit drei ausgerüsteten Angriffen und zwei Passives. Es eignet sich zum Testen, weil es nur die erforderliche `PalID` plus einige gängige Felder enthält.

Das größere Beispiel ist absichtlich extrem. Es zeigt die verfügbare Struktur für Souls, IVs, Skills, Passives und Überschreibungen der Arbeitseignung. Auf Servern mit Importregeln können hohe Werte begrenzt oder blockiert werden.

## Minimalbeispiel

```json
{
    "PalID": "Anubis",
    "Nickname": "Arena Anubis",
    "Gender": "None",
    "Level": 50,
    "PartnerSkillLevel": 1,
    "HP": 3500,
    "SAN": 100,
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "RockLance"
    ],
    "Passives": [
        "Legend",
        "CraftSpeed_up3"
    ]
}
```

## Beispiel

Diese Datei muss hier gespeichert werden: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate` kann ein beliebiger eindeutiger Name in diesem Ordner sein. Das ist später das Befehlsargument für `/givepal_j` und `/spawnpal_j`!)

```json
{
    "PalID": "Anubis",
    "Nickname": "OPnubis",
    "Gender": "None",
    "Level": 255,
    "Shiny": true,
    "PartnerSkillLevel": 255,
    "HP": 999999,
    "SP": 999999,
    "MP": 999999,
    "Hunger": 999999,
    "MaxHunger": 999999,
    "SAN": 999999,
    "Support": 999999,
    "CraftSpeed": 999999,
    "PalSouls": {
        "Health": 255,
        "Attack": 255,
        "Defense": 255,
        "CraftSpeed": 255
    },
    "IVs": {
        "Health": 255,
        "AttackMelee": 255,
        "AttackShot": 255,
        "Defense": 255
    },
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "Unique_Anubis_LowRoundKick"
    ],
    "Passives": [
        "Legend",
        "PAL_ALLAttack_up3",
        "Deffence_up3",
        "Vampire",
        "Stamina_Up_3",
        "EternalFlame",
        "PAL_Sanity_Down_3",
        "Invader",
        "SwimSpeed_up_3",
        "Rare",
        "Nushi",
        "PAL_FullStomach_Down_3",
        "CraftSpeed_up3",
        "Salvation",
        "Witch",
        "MoveSpeed_up_3",
        "SwimSpeed_up_2",
        "CraftSpeed_up2",
        "Deffence_up2",
        "ElementBoost_Normal_2_PAL",
        "PAL_FullStomach_Down_2",
        "ElementBoost_Dragon_2_PAL",
        "ElementBoost_Earth_2_PAL",
        "PAL_ALLAttack_up2",
        "ElementBoost_Fire_2_PAL",
        "ElementBoost_Ice_2_PAL",
        "Stamina_Up_1",
        "TrainerLogging_up1",
        "ElementBoost_Thunder_2_PAL",
        "ElementBoost_Aqua_2_PAL",
        "ElementBoost_Dark_2_PAL",
        "TrainerMining_up1",
        "TrainerWorkSpeed_UP_1",
        "SalePrice_Up_1",
        "Test_PalEgg_HatchingSpeed_Up",
        "MoveSpeed_up_2",
        "CoolTimeReduction_Up_1",
        "ElementBoost_Leaf_2_PAL",
        "TrainerDEF_UP_1",
        "TrainerATK_UP_1",
        "PAL_Sanity_Down_2",
        "ElementResist_Normal_1_PAL",
        "ElementBoost_Dragon_1_PAL",
        "ElementResist_Leaf_1_PAL",
        "PAL_ALLAttack_up1",
        "ElementBoost_Thunder_1_PAL",
        "ElementResist_Dark_1_PAL",
        "ElementBoost_Ice_1_PAL",
        "PAL_FullStomach_Down_1",
        "ElementResist_Dragon_1_PAL",
        "ElementResist_Earth_1_PAL",
        "SalePrice_Up_2",
        "Stamina_Up_2",
        "ElementBoost_Leaf_1_PAL",
        "Deffence_up1",
        "ElementResist_Ice_1_PAL",
        "ElementBoost_Aqua_1_PAL",
        "CoolTimeReduction_Up_2",
        "ElementResist_Thunder_1_PAL",
        "MoveSpeed_up_1",
        "Alien",
        "PAL_Sanity_Down_1",
        "ElementBoost_Earth_1_PAL",
        "ElementBoost_Fire_1_PAL",
        "CraftSpeed_up1",
        "SwimSpeed_up_1",
        "ElementResist_Fire_1_PAL",
        "ElementBoost_Dark_1_PAL",
        "ElementResist_Aqua_1_PAL",
        "ElementBoost_Normal_1_PAL"
    ],
    "ExtraWorkSuitabilities": {
        "EmitFlame": 5,
        "Watering": 5,
        "Seeding": 5,
        "GenerateElectricity": 5,
        "Handcraft": 5,
        "Collection": 5,
        "Deforest": 5,
        "Mining": 5,
        "OilExtraction": 5,
        "ProductMedicine": 5,
        "Cool": 5,
        "Transport": 5,
        "MonsterFarm": 5,
        "Anyone": 5
    }
}
```
