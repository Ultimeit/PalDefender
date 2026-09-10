# 📄 `PalTemplate.json`

utilisez <https://paldeck.cc/creator> pour créer ces fichiers beaucoup plus facilement !

!!! tip "Recherche d'identité"
    Utilisez [paldeck.cc/pals](https://paldeck.cc/pals) pour `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) pour `Passives` et [paldeck.cc/skills](https://paldeck.cc/skills) pour `ActiveSkills` et `LearntSkills`.

| Clé | Type | Descriptif                                                                         |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID` | string | ID interne du Pal à générer. Recherchez des valeurs [`PalID`](https://paldeck.cc/pals) valides sur Paldeck. |
| `UniqueNPCID` | string | ID interne du Pal pour générer des PNJ.                                               |
| `Nickname` | string | Surnom facultatif donné au Pal.                                                 |
| `SkinId` | string | Remplacement du skin pour le Pal (utilisé pour les apparences personnalisées). Utilisez cmd `/getskinids` pour récupérer les identifiants. |
| `Gender` | string | `"Male"`, `"Female"` ou `"None"`.                                                   |
| `Level` | entier | Le niveau du pal.                                                               |
| `Exp` | entier | Points d'expérience.                                                                  |
| `Shiny` | bool | Si le Pal est brillant.                                                           |
| `PartnerSkillLevel` | entier | Niveau de compétence partenaire du Pal. Ne peut pas être inférieur à 1 !                           |
| `CondensedPals` | entier | Nombre de Pals merged/condensed dans celui-ci.                                      |
| `UnusedStatusPoints` | entier | Points d'état disponibles pour la distribution manuelle. Probablement utilisé uniquement pour les joueurs ?    |
| `FriendshipPoints` | entier | Valeur d'amitié pour le Pal.                                               |
| `PhysicalHealth` | string | État de santé physique. Les noms valides incluent `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick` | string | État de maladie des travailleurs. Les noms valides incluent `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter` | bool | Marque le Pal comme caractère importé.                                    |
| `HP` / `SP` / `MP` | numéro | Valeurs de base de santé, d'endurance et de mana. `HP` définit les PV maximum du Pal généré, y compris pour les invocations PalSummon et REST qui référencent ce modèle. |
| `Shield` | numéro | Valeur du bouclier.                                                              |
| `Hunger` / `MaxHunger` | entier | Valeurs de faim actuelles et maximales.                                                      |
| `SAN` | entier | Santé mentale (stabilité mentale du Pal).                                               |
| `Support` | entier | Niveau de support (utilisé pour le comportement et les compétences de l'IA).                                    |
| `CraftSpeed` | entier | Multiplicateur de vitesse de fabrication.                                                          |
| `PalSouls` | object | Bonus d'âme passive. Contient : `Health`, `Attack`, `Defense`, `CraftSpeed`. Les valeurs normales recommandées sont contrôlées par vos règles d'importation. |
| `IVs` | object | Valeurs de statistiques individuelles. Contient : `Health`, `AttackMelee`, `AttackShot`, `Defense`. Les valeurs normales recommandées sont contrôlées par vos règles d'importation. |
| `ActiveSkills` | array | Liste des compétences équipées. PalDefender 1.9.0 ne tronque pas les PalTemplates d'administration à trois entrées ; chaque entrée reste équipée. Recherchez des [ID de compétence](https://paldeck.cc/skills) valides sur Paldeck. Le comportement normal de game/UI peut toujours supposer le nombre d'emplacements standard. |
| `LearntSkills` | array | Compétences que le Pal a acquises et vers lesquelles il peut échanger. Évitez de mettre des compétences actives ici. Recherchez des [ID de compétence](https://paldeck.cc/skills) valides sur Paldeck. |
| `Passives` | array | Traits passifs du Pal. Le Pals normal devrait utiliser jusqu'à 4 passifs. Recherchez des valeurs [`PassiveID`](https://paldeck.cc/passives) valides sur Paldeck. |
| `ExtraWorkSuitabilities` | object | Types et niveaux de travail améliorés (par exemple, `"Mining": 2`). Types de travaux disponibles : `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`.  |
| `DisableWorkPreferences` | array | Types de travaux que le Pal refuse de faire. Types de travaux disponibles : `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Jeu d'instructions

1. Créez un fichier JSON par Pal personnalisé dans `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Utilisez un nom de fichier unique, par exemple `RaidRewardAnubis.json`. Les commandes peuvent généralement utiliser `RaidRewardAnubis` ou `RaidRewardAnubis.json`.
3. Incluez toujours `PalID`. Tout le reste est facultatif, mais les valeurs manquantes utilisent les valeurs par défaut PalDefender ou Palworld.
4. Gardez `Level` à `1` ou plus et `PartnerSkillLevel` à `1` ou plus.
5. Placez les attaques équipées dans `ActiveSkills` et les autres attaques connues dans `LearntSkills`. PalDefender ne déplace plus les entrées actives supplémentaires vers les compétences apprises.
6. Utilisez des identifiants exacts pour Pals, les compétences, les passifs, les skins et les types de travail. Les identifiants erronés peuvent échouer à l'importation ou être ignorés.
7. Validez JSON avant de télécharger. JSON n'autorise pas les commentaires ni les virgules finales.
8. Si un modèle est importé mais que les valeurs sont modifiées ou bloquées, vérifiez le `Pals/ImportRules/Default.json` du serveur et tous les fichiers de remplacement par-Pal.

## Procédure pas à pas de configuration

1. Décidez à quoi sert le modèle : une simple récompense d'administrateur, un boss d'événement, un Pal de test ou un modèle d'apparition pour une invocation.
2. Choisissez le `PalID` à [paldeck.cc/pals](https://paldeck.cc/pals). Le nom d'affichage n'est pas toujours l'ID du fichier, copiez donc exactement l'ID.
3. Ajoutez uniquement les champs que vous souhaitez contrôler. Un modèle court est plus facile à déboguer qu’un très grand modèle.
4. Choisissez des compétences sur [paldeck.cc/skills](https://paldeck.cc/skills). Placez les attaques équipées dans `ActiveSkills` ; ajoutez les autres attaques connues à `LearntSkills`.
5. Choisissez les passifs parmi [paldeck.cc/passives](https://paldeck.cc/passives). Pour une utilisation normale, conservez jusqu'à quatre passifs, sauf si votre serveur en autorise intentionnellement davantage.
6. Enregistrez le fichier dans `Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
7. Testez d'abord avec `/givemepal_j <filename>`. Après cela, utilisez le même modèle pour `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, le REST API ou `PalSummon.json`.

## Exemples d'explications

L'exemple minimal ci-dessous crée un Anubis de niveau 50 avec trois attaques équipées et deux passifs. Il convient aux tests car il ne contient que le `PalID` requis ainsi que quelques champs communs.

L’exemple le plus vaste est intentionnellement extrême. Il montre la structure disponible pour les âmes, les IV, les compétences, les passifs et les remplacements d'aptitude au travail. Sur les serveurs utilisant des règles d'importation, les valeurs élevées peuvent être limitées ou bloquées.

## Exemple minimal

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

## Exemple

Ce fichier doit être stocké à l'adresse : `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate` peut être n'importe quel nom unique dans ce dossier. Ce sera l'argument de commande pour `/givepal_j` et `/spawnpal_j` !)

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
