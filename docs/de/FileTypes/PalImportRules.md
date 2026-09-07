# 📄 `Pals/ImportRules/*.json`


Pal-Importregeln steuern, welche `PalTemplate.json`-Dateien beim Import über Befehle oder API-Aktionen erlaubt, blockiert oder angepasst werden.

!!! tip "ID-Suche"
    Nutze [paldeck.cc/pals](https://paldeck.cc/pals) für `AllowedPalIDs`, `BannedPalIDs` und Dateinamen für Pal-spezifische Regeln. Nutze [paldeck.cc/passives](https://paldeck.cc/passives) für `DisallowedPassives`.

## Dateipfade

| Datei | Zweck |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | Globale Importregeln für alle Pal-Templates. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | Optionale Pal-spezifische Überschreibung. Suche die [`PalID`](https://paldeck.cc/pals) auf Paldeck und nutze genau diese ID als Dateinamen. Beispiel: `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | Als Referenz generierte Beispieldatei. Sie ist erst eine echte Pal-Regel, wenn sie kopiert und umbenannt wurde. |

## Schlüssel

| Schlüssel | Typ | Beschreibung |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | Nur in `Default.json`. `AllowAllExceptBanned` erlaubt alle Pals außer `BannedPalIDs`. `AllowOnlyListed` erlaubt nur `AllowedPalIDs`. |
| `AllowedPalIDs` | array | Nur in `Default.json`. [`PalID`](https://paldeck.cc/pals)-Werte, die bei `PalSelectionMode: "AllowOnlyListed"` erlaubt sind. |
| `BannedPalIDs` | array | Nur in `Default.json`. [`PalID`](https://paldeck.cc/pals)-Werte, die immer abgelehnt werden. |
| `MaxValueLimitAction` | string | `BlockImport` lehnt Templates oberhalb der konfigurierten Limits ab. `ClampToMaxValues` reduziert Werte auf die konfigurierten Limits. |
| `DisallowedPassivesAction` | string | `BlockImport` lehnt Templates mit gelisteten Passives ab. `RemoveFromPal` entfernt gelistete Passives vor dem Import. |
| `DisallowedPassives` | array | [`PassiveID`](https://paldeck.cc/passives)-Werte, auf die `DisallowedPassivesAction` angewendet wird. |
| `ConditionMode` | string | `None` wendet die Regel normal an. `RequirePalCaptureCount` erlaubt den Import erst, nachdem der Spieler genügend Pals derselben Art gefangen hat. |
| `RequiredCaptureCount` | int | Erforderliche Fangzahl derselben Art für `RequirePalCaptureCount` (Standard: `5`). |
| `Disabled` | bool | Wenn `true`, werden Importprüfungen für dieses Regelset deaktiviert. |
| `BanIfPalIsImpossible` | bool | Wenn `true`, kann PalDefender unmögliche Pal-Importe gemäß Servereinstellungen bestrafen. |
| `AllowGenderNone` | bool | Wenn `false`, können Templates mit `Gender: "None"` durch Importprüfungen abgelehnt werden. |
| `MaxLevel` | int | Höchstes erlaubtes Pal-Level für importierte Templates. |
| `MaxRank` | int | Höchster erlaubter Partner-Skill-Rang für importierte Templates. |
| `PalSouls` | object | Maximal erlaubte Pal-Soul-Werte: `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | object | Maximal erlaubte IV-Werte: `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## Anleitung

1. Beginne mit `Default.json`. Nutze sie für serverweite Regeln.
2. Nutze Dateien pro Pal nur, wenn ein bestimmter Pal andere Limits braucht.
3. Pal-spezifische Dateien müssen nach der Pal-ID benannt werden, zum Beispiel `Anubis.json`.
4. Setze `PalSelectionMode`, `AllowedPalIDs` und `BannedPalIDs` nicht in Pal-spezifische Dateien. Diese Werte gehören in `Default.json`.
5. Nutze `BlockImport`, wenn du strikte Moderation willst.
6. Nutze `ClampToMaxValues`, wenn du Templates akzeptieren, aber zu hohe Werte reduzieren willst.
7. Nutze `RemoveFromPal` für Passives, wenn du automatische Bereinigung statt fehlgeschlagenem Import bevorzugst.
8. IDs müssen exakt stimmen. Validiere JSON, bevor du es hochlädst.

## Einrichtungsschritte

1. Öffne oder erstelle `Pals/ImportRules/Default.json`.
2. Lege die globale Pal-Regel fest:
   - Nutze `AllowAllExceptBanned`, wenn die meisten Pals erlaubt sind und du nur wenige blockieren willst.
   - Nutze `AllowOnlyListed`, wenn Importe auf eine kuratierte Liste beschränkt werden sollen.
3. Lege fest, wie streng moderiert werden soll:
   - Nutze `BlockImport` für strikte Server, auf denen ungültige Templates fehlschlagen sollen.
   - Nutze `ClampToMaxValues`, wenn du Templates akzeptieren, aber zu hohe Level, Ranks, Souls oder IVs reduzieren willst.
   - Nutze `RemoveFromPal` für Passives, wenn du unerwünschte Passives entfernen statt das gesamte Template ablehnen willst.
4. Füge unerlaubte Passives von [paldeck.cc/passives](https://paldeck.cc/passives) hinzu.
5. Füge gebannte oder erlaubte Pals von [paldeck.cc/pals](https://paldeck.cc/pals) hinzu.
6. Lege eine Pal-spezifische Überschreibung nur an, wenn ein bestimmter Pal strengere oder lockerere Limits braucht als die globale Datei.
7. Teste zuerst mit einer kleinen `PalTemplate.json`, bevor du große Templates importierst.

## Häufige Setups

### Die meisten Pals erlauben, einige blockieren

Nutze das, wenn normale Admin-Belohnungen erlaubt sind, bestimmte Pals aber nicht importiert werden sollen.

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "BannedPalIDs": [
        "JetDragon",
        "BOSS_Anubis"
    ],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

### Nur eine kuratierte Liste erlauben

Nutze das, wenn von Spielern importierte Templates auf freigegebene Pals beschränkt werden sollen.

```json
{
    "PalSelectionMode": "AllowOnlyListed",
    "AllowedPalIDs": [
        "Anubis",
        "Kirin",
        "WeaselDragon"
    ],
    "BannedPalIDs": [],
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 50,
    "MaxRank": 4,
    "PalSouls": {
        "Health": 10,
        "Attack": 10,
        "Defense": 10,
        "CraftSpeed": 10
    },
    "IVs": {
        "Health": 80,
        "AttackMelee": 80,
        "AttackShot": 80,
        "Defense": 80
    }
}
```

In diesem Setup können nur die drei gelisteten `PalID`-Werte importiert werden. Werte oberhalb der Limits werden auf die konfigurierten Maximalwerte reduziert, und die gelisteten Passives werden vom Pal entfernt.

## Standardbeispiel

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "BannedPalIDs": [
        "JetDragon"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

## Beispiel für eine Pal-spezifische Überschreibung

### `Anubis.json`
```json
{
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "AllowGenderNone": false,
    "MaxLevel": 10,
    "MaxRank": 3,
    "PalSouls": {
        "Health": 5,
        "Attack": 5,
        "Defense": 5,
        "CraftSpeed": 5
    },
    "IVs": {
        "Health": 50,
        "AttackMelee": 50,
        "AttackShot": 50,
        "Defense": 50
    }
}
```
