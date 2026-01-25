# 📄 `PalTemplate.json`

Verwende <https://paldeck.cc/palcreator>, um diese Dateien **deutlich einfacher** zu erstellen!

| Key                      | Typ    | Beschreibung                                                                 |
| ------------------------ | ------ | ----------------------------------------------------------------------------- |
| `PalID`                  | string | Interne ID des zu spawnenden Pals. Verwende [diese Liste](https://paldeck.cc/pals), um die IDs zu finden. |
| `UniqueNPCID`            | string | Interne ID zur Erstellung von Pal-NPCs.                                      |
| `Nickname`               | string | Optionaler Spitzname für den Pal.                                            |
| `SkinId`                 | string | Skin-Override für den Pal (benutzerdefiniertes Aussehen). Verwende den Befehl `/getskinids`, um verfügbare IDs abzurufen. |
| `Gender`                 | string | `"Male"`, `"Female"` oder `"None"`.                                          |
| `Level`                  | int    | Level des Pals.                                                              |
| `Exp`                    | int    | Erfahrungspunkte.                                                            |
| `Shiny`                  | bool   | Gibt an, ob der Pal shiny ist.                                                |
| `PartnerSkillLevel`      | int    | Level der Partnerfähigkeit des Pals. Darf **nicht kleiner als 1** sein!      |
| `CondensedPals`          | int    | Anzahl der in diesen Pal kondensierten/verschmolzenen Pals.                 |
| `UnusedStatusPoints`     | int    | Verfügbare Statuspunkte zur manuellen Verteilung. Vermutlich nur für Spieler relevant. |
| `HP` / `SP` / `MP`       | int    | Basiswerte für Leben, Ausdauer und Mana.                                     |
| `Hunger` / `MaxHunger`   | int    | Aktueller und maximaler Hungerwert.                                          |
| `SAN`                    | int    | Sanity (geistige Stabilität des Pals).                                       |
| `Support`                | int    | Support-Level (beeinflusst KI-Verhalten und Fähigkeiten).                    |
| `CraftSpeed`             | int    | Multiplikator für die Herstellungsgeschwindigkeit.                           |
| `PalSouls`               | object | Passive Seelenboni. Enthält: `Health`, `Attack`, `Defense`, `CraftSpeed`. (0–255) |
| `IVs`                    | object | Individuelle Statuswerte. Enthält: `Health`, `AttackMelee`, `AttackShot`, `Defense`. (0–255) |
| `ActiveSkills`           | array  | Liste der aktuell ausgerüsteten Fähigkeiten (max. 3). Verwende [diese Liste](https://paldeck.cc/skill), um die IDs zu finden. |
| `LearntSkills`           | array  | Erlernte Fähigkeiten, zu denen der Pal wechseln kann. (Aktive Skills hier möglichst vermeiden.) Verwende [diese Liste](https://paldeck.cc/skill). |
| `Passives`               | array  | Passive Eigenschaften des Pals. Verwende [diese Liste](https://paldeck.cc/passives), um die IDs zu finden. |
| `ExtraWorkSuitabilities` | object | Verstärkte Arbeitsarten und -level (z. B. `"Mining": 2`). Verfügbare Arbeiten: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |
| `DisableWorkPreferences` | array  | Arbeitsarten, die der Pal verweigert. Verfügbare Arbeiten: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Beispiel:

Diese Datei muss unter folgendem Pfad gespeichert werden:
`<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate` kann ein beliebiger eindeutiger Name in diesem Ordner sein. Dieser Name wird als Befehlsargument für `/givepal_j` und `/spawnpal_j` verwendet!)

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
