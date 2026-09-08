# 📄 `Pals/ImportRules/*.json`


Les règles d'importation Pal contrôlent quels fichiers `PalTemplate.json` sont autorisés, bloqués ou ajustés lorsqu'ils sont importés par des commandes ou des actions API.

!!! tip "Recherche d'identité"
    Utilisez [paldeck.cc/pals](https://paldeck.cc/pals) pour les noms de fichiers de règles `AllowedPalIDs`, `BannedPalIDs` et par-Pal. Utilisez [paldeck.cc/passives](https://paldeck.cc/passives) pour `DisallowedPassives`.

## Emplacements des fichiers

| Fichier | Objectif |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | Règles d'importation globales pour tous les modèles Pal. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | Remplacement facultatif par-Pal. Recherchez le [`PalID`](https://paldeck.cc/pals) sur Paldeck, puis utilisez cet identifiant exact comme nom de fichier. Exemple : `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | Exemple de fichier généré pour référence. Ce n'est pas une véritable règle Pal tant qu'elle n'est pas copiée et renommée. |

## Clés

| Clé | Type | Descriptif |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | `Default.json` uniquement. `AllowAllExceptBanned` autorise tous les Pal sauf `BannedPalIDs`. `AllowOnlyListed` autorise uniquement `AllowedPalIDs`. |
| `AllowedPalIDs` | array | `Default.json` uniquement. [`PalID`](https://paldeck.cc/pals) valeurs autorisées lorsque `PalSelectionMode` est `AllowOnlyListed`. |
| `BannedPalIDs` | array | `Default.json` uniquement. [`PalID`](https://paldeck.cc/pals) valeurs qui sont toujours refusées. |
| `MaxValueLimitAction` | string | `BlockImport` refuse les modèles dépassant les limites configurées. `ClampToMaxValues` abaisse les valeurs aux limites configurées. |
| `DisallowedPassivesAction` | string | `BlockImport` refuse les modèles avec des passifs répertoriés. `RemoveFromPal` supprime les passifs répertoriés avant l'importation. |
| `DisallowedPassives` | array | [`PassiveID`](https://paldeck.cc/passives) valeurs affectées par `DisallowedPassivesAction`. |
| `ConditionMode` | string | `None` applique la règle normalement. `RequirePalCaptureCount` permet d'importer un Pal seulement après que ce joueur ait capturé suffisamment de Pals de la même espèce. |
| `RequiredCaptureCount` | entier | Nombre de captures de la même espèce requis lorsque `ConditionMode` est `RequirePalCaptureCount` (par défaut `5`). |
| `Disabled` | bool | Si `true`, désactive les vérifications d’importation pour l’ensemble de règles correspondant. |
| `BanIfPalIsImpossible` | bool | Si `true`, PalDefender peut punir les importations Pal impossibles selon les paramètres du serveur. |
| `AllowGenderNone` | bool | Si `false`, les modèles utilisant `Gender: "None"` peuvent être rejetés par les contrôles d'importation. |
| `MaxLevel` | entier | Niveau Pal le plus élevé autorisé pour les modèles importés. |
| `MaxRank` | entier | Classement de compétence partenaire le plus élevé autorisé pour les modèles importés. |
| `PalSouls` | object | Valeurs d'âme Pal maximales autorisées : `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | object | Valeurs IV maximales autorisées : `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## Jeu d'instructions

1. Commencez par `Default.json`. Utilisez-le pour la politique à l'échelle du serveur.
2. Utilisez les fichiers per-Pal uniquement lorsqu'un Pal nécessite des limites différentes.
3. Les fichiers Per-Pal doivent être nommés avec l'ID Pal, par exemple `Anubis.json`.
4. Ne placez pas `PalSelectionMode`, `AllowedPalIDs` ou `BannedPalIDs` dans les fichiers propres à un Pal. Ces clés appartiennent à `Default.json`.
5. Utilisez `BlockImport` si vous souhaitez une modération stricte.
6. Utilisez `ClampToMaxValues` si vous préférez accepter les modèles mais réduire les valeurs dépassées.
7. Utilisez `RemoveFromPal` pour les passifs si vous préférez un nettoyage automatique plutôt qu'une importation ayant échoué.
8. Conservez les identifiants exacts et validez JSON avant de télécharger.

## Procédure pas à pas de configuration

1. Ouvrez ou créez `Pals/ImportRules/Default.json`.
2. Décidez de la politique globale Pal :
   - Utilisez `AllowAllExceptBanned` lorsque la plupart des Pals sont autorisés et que vous ne souhaitez en bloquer que quelques-uns.
   - Utilisez `AllowOnlyListed` lorsque les importations doivent être limitées à une liste organisée.
3. Décidez du style de modération :
   - Utilisez `BlockImport` pour les serveurs stricts sur lesquels les modèles non valides devraient échouer.
   - Utilisez `ClampToMaxValues` lorsque vous souhaitez accepter des modèles mais réduire les niveaux, rangs, âmes ou IV dépassant les limites.
   - Utilisez `RemoveFromPal` pour les passifs lorsque vous souhaitez supprimer les passifs indésirables au lieu de rejeter l'intégralité du modèle.
4. Ajoutez les passifs interdits de [paldeck.cc/passives](https://paldeck.cc/passives).
5. Ajoutez Pals interdit ou autorisé à partir de [paldeck.cc/pals](https://paldeck.cc/pals).
6. Ajoutez un remplacement per-Pal uniquement lorsqu'un Pal spécifique nécessite des limites plus strictes ou plus souples que le fichier global.
7. Testez d'abord avec un petit `PalTemplate.json` avant d'importer de grands modèles.

## Configurations courantes

### Autoriser la plupart des Pals, en bloquer quelques-uns

Utilisez-le lorsque les récompenses administratives normales sont autorisées, mais que certains Pals ne doivent pas être importés.

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

### Autoriser uniquement une liste organisée

Utilisez-le lorsque les modèles importés par le lecteur doivent être limités aux Pals approuvés.

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

Dans cette configuration, seules les trois valeurs `PalID` répertoriées peuvent être importées. Les valeurs de dépassement de limite sont réduites aux maximums configurés et les passifs répertoriés sont supprimés du Pal.

## Exemple par défaut

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

## Exemple de remplacement par-Pal

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
