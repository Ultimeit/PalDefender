# 📄 `PalSummon.json`

Un fichier PalSummon définit une rencontre à emplacement fixe lancée avec `/summon <filename>`. Stockez les fichiers dans `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/` et les PalTemplates référencés dans `Pals/Templates/`.

!!! tip "Recherche d’identifiants"
    Utilisez [paldeck.cc/pals](https://paldeck.cc/pals) pour `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) pour les passifs et [paldeck.cc/skills](https://paldeck.cc/skills) pour les ID de compétences utilisés par le modèle référencé.

## Clés de rencontre

| Clé | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `PalTemplate` | string | Obligatoire | Nom de fichier d'un modèle dans `Pals/Templates/` ; `.json` peut être omis. |
| `BossBattleName` | string | Pal ID | Nom d'affichage utilisé dans les annonces, les journaux, les webhooks et les résultats des dommages. |
| `Uncapturable` | bool | `false` | Empêche le Pal invoqué d'être capturé. |
| `CapturableAtHealthPercent` | numéro | `15` | Si capturable, active la capture uniquement à ce pourcentage de HP ou moins (`0`–`100`). Ignoré lorsque `Uncapturable` est `true`. |
| `DisableAI` | bool | `false` | Désactive l'IA normale. Certains comportements passifs, comme l'esquive, peuvent toujours se produire. |
| `DisableDamageMeter` | bool | `false` | Désactive le suivi, la boîte de dialogue des résultats et les récompenses de classement. La récompense `Default` est plutôt accordée à tous les joueurs en ligne. |
| `SpawnScale` | numéro | `1.0` | Multiplicateur de taille Visual/physical ; les valeurs non positives reviennent à `1.0`. |
| `DamageTakenMultiplier` | numéro | `1.0` | Multiplicateur des dommages reçus ; les valeurs négatives reviennent à `1.0`. |
| `DamageDealtMultiplier` | numéro | `1.0` | Multiplicateur des dégâts infligés ; les valeurs négatives reviennent à `1.0`. |
| `X`, `Y`, `Z` | numéro | Obligatoire | Coordonnées de la carte. Utilisez `/getpos` pour les obtenir. |
| `DisableStatuses` | array | Vide | Noms de statut à supprimer. Les noms invalides sont ignorés. |
| `Rewards` | object ou array | Vide | [Définitions de récompenses propres au classement et par défaut](#damage-meter-and-rewards) facultatives. Le format object est recommandé. |

`CapturableAt`, `CapturableAtPercent` et `capturable_at` sont des alias de compatibilité acceptés. `AdditionalEnemyReceiveDamageRate` et `AdditionalEnemyInflictDamageRate` sont également acceptés, mais les noms du tableau sont préférés.

!!! warning "Migration des PV maximum"
    Les PV maximum du Pal invoqué proviennent désormais de `HP` dans le PalTemplate référencé. `HealthMultiplier`, `HPMultiplier` et `AdditionalEnemyMaxHPRate` ne sont plus pris en charge ; supprimez ces champs des fichiers PalSummon existants.

## Compteur de dégâts et récompenses { #damage-meter-and-rewards }

Les récompenses sont résolues après la mort ou la capture du Pal invoqué. Le classement des dégâts est trié du plus élevé au plus faible. La boîte de dialogue des résultats affiche les cinq premiers, met en évidence les trois premiers et affiche également la propre position du joueur qui reçoit lorsque ce joueur est en dehors du top cinq.

Lorsque le suivi des dégâts est activé, chaque joueur participant est traité comme suit :

1. PalDefender recherche une clé numérique `Rewards` correspondant au rang final de ce joueur.
2. Si ce rang exact n'existe pas, PalDefender utilise `Rewards.Default`.
3. Si aucun des deux n’existe, ce joueur ne reçoit aucune récompense.
4. La récompense sélectionnée est lancée séparément pour ce joueur. Deux joueurs utilisant la même définition `Default` peuvent donc recevoir des résultats aléatoires différents.

Seuls les participants qui sont toujours en ligne et disposent d'une manette de joueur disponible à la fin de la rencontre peuvent recevoir des récompenses classées. Une récompense numérotée n'inclut pas la récompense `Default` ; il le remplace pour ce rang.

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

Dans cet exemple, la première place reçoit les deux récompenses garanties, la deuxième place reçoit un montant aléatoire d'EXP et tous les autres participants classés ont indépendamment 75 % de chances de recevoir 1 000 argent.

Les clés de classement doivent être des nombres entiers positifs écrits sous la forme de clés JSON object, telles que `"1"`, `"2"` ou `"10"`. `"0"`, les classements négatifs et les noms arbitraires ne sont pas valides. `Default` ne respecte pas la casse.

??? note "Formulaire Array"
    `Rewards` peut également être un array. Array l'élément 0 est de rang 1, l'élément 1 est de rang 2, et ainsi de suite. Le formulaire array ne peut pas définir `Default`, le formulaire object est donc plus clair et est recommandé.

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### Structure de définition des récompenses

Chaque rang et `Default` contiennent une définition de récompense. Une définition peut contenir à la fois :

- `Drops` : entrées évaluées directement et indépendamment.
- `Pools` : groupes qui contrôlent la manière dont les entrées sont sélectionnées.

Il peut également contenir les raccourcis de progression `EXP`, `TechnologyPoints` et `AncientTechnologyPoints`. Les raccourcis sont garantis et sont utiles lorsqu'ils n'ont pas besoin de leur propre paramètre `Chance`, `Weight` ou `Unique`.

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

### Types de participation aux récompenses

Chaque entrée doit définir exactement un type de récompense. Ne combinez pas un champ d'objet, d'œuf et de progression dans la même entrée.

| Récompense | Champs obligatoires | Champs optionnels | Remarques |
| --- | --- | --- | --- |
| Article | `ItemID` | `Count`, `Chance`, `Weight`, `Unique` | `Count` est par défaut `1`. |
| Pal oeuf | `EggID`, `PalTemplate` | `Count`, `Level`, `Chance`, `Weight`, `Unique` | `Count` est par défaut `1` ; `Level: 0` utilise le niveau du modèle. |
| Expérience | `EXP` | `Chance`, `Weight`, `Unique` | La valeur `EXP` est le montant ou la plage. |
| Points technologiques | `TechnologyPoints` | `Chance`, `Weight`, `Unique` | La valeur du champ est le montant ou la plage. |
| Points de technologie ancienne | `AncientTechnologyPoints` | `Chance`, `Weight`, `Unique` | La valeur du champ est le montant ou la plage. |

`Chance`, `Weight` et `Unique` ne sont efficaces que dans les contextes décrits ci-dessous. Un champ accepté par l'analyseur ne signifie pas qu'il affecte tous les modes de distribution.

Les noms de champs canoniques ci-dessus sont recommandés. L'analyseur accepte également ces alias :

| Champ canonique | Alias acceptés |
| --- | --- |
| `ItemID` | `ItemId`, `ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`, `Num` |
| `EXP` | `Exp`, `Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### Valeurs fixes, plages et chances

Les montants peuvent être un nombre entier fixe ou une plage inclusive :

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

- Les montants de `Count`, d'EXP et de points technologiques doivent être des nombres entiers d'au moins `1`.
- Une plage nécessite à la fois `Min` et `Max`, et `Max` ne doit pas être inférieur à `Min`.
- Les plages de texte telles que `"1-3"` ne sont pas valides ; utilisez `{ "Min": 1, "Max": 3 }`.
- L'œuf `Level` peut être `0` ; cela conserve le niveau du PalTemplate référencé. Un niveau positif remplace le niveau du modèle et est plafonné au niveau 255 lorsque l'œuf est accordé.
- `Chance` accepte un nombre ou un texte numérique avec un `%` facultatif, par exemple `30`, `30.5` ou `"30%"`.
- `Chance: 0` ne réussit jamais, `Chance: 100` réussit toujours et les valeurs doivent rester entre `0` et `100`.
- Pour une chance strictement comprise entre 0 et 100, le jet généré doit être inférieur à la valeur configurée. Un jet de `30.0` exactement échoue donc à un `Chance` de `30`.

### Chutes directes

Chaque entrée dans `Drops` est évaluée indépendamment. Il n’y a pas de relation de choix entre les entrées voisines. `Chance` manquant signifie `100`.

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

L'argent est garanti. Les munitions, l'EXP et les points technologiques font chacun leur propre jet de chance. Zéro, un, deux ou les trois largages facultatifs peuvent réussir.

`Weight` et `Unique` ne fonctionnent pas en direct `Drops` et produisent des avertissements. Utilisez `Chance` pour les dépôts directs facultatifs.

## Pools de butin

Un pool lance d’abord son propre `Chance`. Si le pool échoue, aucune de ses entrées n’est prise en compte. En cas de succès, `Mode` décide de la manière dont les entrées sont évaluées.

| Clé du pool | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `Name` | string | Vide | Étiquette de diagnostic en option. Cela n'affecte pas la sélection. |
| `Mode` | string | `OneOf` | `OneOf`, `Pick`, `All` ou `Independent`. La correspondance n'est pas sensible à la casse. |
| `Chance` | texte en nombre ou en pourcentage | `100` | Chance que toute la piscine s'active. |
| `Rolls` | nombre entier | `1` | Nombre de sélections dans `Pick` ; ignoré par les autres modes. |
| `Unique` | bool | `true` | Politique de répétition par défaut pour `Pick` ; une entrée peut le remplacer. |
| `Entries` | array | Obligatoire | Liste non vide des entrées de récompenses. |

`One` est accepté comme alias pour `OneOf` et `PickN` comme alias pour `Pick`, mais les noms de mode canoniques sont recommandés.

| Mode | Combien d’entrées peuvent être accordées ? | Utilise `Weight` ? | Utilise l'entrée `Chance` ? | Utilise `Rolls` / `Unique` ? |
| --- | --- | --- | --- | --- |
| `OneOf` | Exactement un si le pool réussit | Oui | Non | Non |
| `Pick` | Jusqu'à `Rolls` sélections | Oui | Non | Oui |
| `All` | Chaque entrée une fois si le pool réussit | Non | Non | Non |
| `Independent` | Zéro dans toutes les entrées | Non | Oui | Non |

Les quatre modes utilisent toujours le `Chance` au niveau du pool. Plusieurs pools dans une définition de récompense sont traités indépendamment et leurs résultats sont ajoutés au `Drops` direct.

### `OneOf` : un résultat pondéré

`OneOf` est le mode par défaut. Si sa chance au niveau du pool réussit, exactement une entrée est sélectionnée. La probabilité d'une entrée est son `Weight` divisé par la somme de tous les poids d'entrée.

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

Les pondérations totalisent 20. Sous réserve que le pool réussisse, les quatre entrées ont des probabilités de 35 %, 35 %, 25 % et 5 %. Étant donné que la piscine elle-même ne s'active que 35 % du temps, la chance absolue de l'œuf est de `35% × 5% = 1.75%`.

- `Weight` manquant est par défaut `1`.
- `Weight` doit être un nombre entier d'au moins `1` ; supprimer une entrée au lieu d'attribuer un poids `0`.
- `Rolls` est ignoré et produit un avertissement car `OneOf` sélectionne toujours une fois.
- Le niveau d'entrée `Chance` est ignoré et produit un avertissement. Utilisez `Weight` pour contrôler la probabilité de sélection relative.
- `Unique` n'a aucun effet pratique car une seule entrée est sélectionnée.

### `Pick` : plusieurs résultats pondérés sans répétitions

`Pick` répète la sélection pondérée `Rolls` fois. Avec la valeur par défaut `Unique: true`, une entrée sélectionnée est supprimée avant la sélection suivante et ne peut pas être sélectionnée à nouveau. Les poids sont recalculés à partir des entrées restantes après chaque sélection.

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

Cela accorde deux entrées différentes. Si `Rolls` est supérieur au nombre d'entrées uniques disponibles, la sélection s'arrête lorsqu'il ne reste aucune entrée ; ce n'est pas une erreur.

### `Pick` : permettre des résultats répétés

Définissez le `Unique` du pool sur `false` pour conserver les entrées sélectionnées disponibles pour les lancers ultérieurs. Les subventions répétées du même objet sont fusionnées avant la livraison.

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

Les trois lancers peuvent sélectionner de l'argent, tous peuvent sélectionner des munitions ou les résultats peuvent être mitigés. Par exemple, sélectionner Money deux fois produit une subvention Money de 10 000 plutôt que deux subventions distinctes.

### `Pick` : remplacement de `Unique` par entrée

Un `Unique` d’entrée remplace la valeur par défaut du pool uniquement pour cette entrée. Cela permet des récompenses communes reproductibles et des récompenses de jackpot uniques dans le même pool.

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

L'argent reste dans la liste des candidats après avoir été sélectionné car son entrée indique `Unique: false`. L'armure et le casque héritent de `Unique: true` du pool et sont retirés après sélection. L'inverse est également valable : un pool peut utiliser `Unique: false` tandis qu'une entrée particulière utilise `Unique: true`.

### `All` : accorder chaque entrée

`All` accorde chaque entrée exactement une fois lorsque le `Chance` au niveau du pool réussit.

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

`Weight`, `Chance` d'entrée de gamme et `Unique` n'affectent pas `All`. `Rolls` est ignoré et produit un avertissement. Pour rendre l'ensemble du bundle facultatif, définissez le `Chance` du pool ; pour rendre les entrées individuelles facultatives, utilisez plutôt `Independent` ou directement `Drops`.

### `Independent` : lancer chaque entrée séparément

`Independent` vérifie chaque entrée et utilise le `Chance` de chaque entrée. Il peut n'accorder aucune entrée, une entrée, plusieurs entrées ou toutes les entrées.

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

Premièrement, le pool a 80 % de chances de s’activer. S'il s'active, Money est garanti car son entrée omet `Chance` ; les trois autres entrées lancent indépendamment 50 %, 10 % et 5 %.

- L'entrée manquante `Chance` est par défaut `100`.
- `Weight` et `Unique` n'affectent pas ce mode.
- `Rolls` est ignoré et produit un avertissement car chaque entrée est vérifiée une fois.

### Combinaison de dépôts directs et de plusieurs pools

Utilisez plusieurs pools lorsqu'un destinataire doit recevoir plusieurs niveaux de récompenses structurés indépendamment.

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

L'argent direct et l'EXP s'appliquent toujours. Le premier pool ajoute un élément d'équipement, le second effectue deux sélections de ravitaillement pondérées avec remplacement et le troisième effectue deux jets de bonus indépendants. Un joueur peut recevoir les résultats de chaque pool car les pools ne se font pas concurrence.

### Pal récompenses en œufs

Un œuf a besoin à la fois de `EggID` et de `PalTemplate`. Le modèle est chargé à partir de `Pals/Templates/` et `.json` peut être omis. `Count` contrôle le nombre d'œufs accordés. `Level: 0` ou un niveau omis conserve le niveau du modèle ; une valeur fixe ou une plage positive la remplace.

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

Si un modèle d'œuf ne peut pas être importé lorsque la récompense est accordée, PalDefender enregistre une erreur et ignore cette récompense d'œuf.

### Fusionner des résultats répétés

Les résultats des drops directs et de tous les pools sont combinés avant la livraison :

- Les éléments avec le même `ItemID` sont fusionnés en additionnant leurs nombres.
- Les œufs ne fusionnent que lorsque `EggID`, `PalTemplate` et le `Level` obtenu sont tous identiques.
- L'EXP, les points technologiques et les points technologiques anciens sont additionnés.
- Les totaux des éléments pouvant être accordés et des points technologiques sont limités au maximum signé de 32 bits (`2,147,483,647`).

Cela signifie que les résultats `Pick` répétés ne créent pas de lignes d'inventaire en double dans la demande de récompense. Les œufs avec différents niveaux roulés restent des récompenses distinctes.

### répartition `DisableDamageMeter`

Lorsque `DisableDamageMeter` est `true`, PalDefender ne crée pas de classement des dégâts et n'utilise pas de récompenses de rang numérique. Au lieu de cela, il lance `Rewards.Default` séparément pour **chaque joueur qui est en ligne à la fin de la rencontre**, y compris les joueurs qui n'ont pas endommagé le Pal invoqué.

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

L'argent est accordé à chaque joueur en ligne. Chaque joueur lance indépendamment les deux récompenses facultatives en points. Si `Default` est manquant ou vide, personne ne reçoit de récompense dans ce mode et PalDefender écrit un avertissement dans le journal.

### Combinaisons invalides et ignorées

Des données de récompense non valides empêchent le chargement du fichier PalSummon. Les champs inconnus ou ignorés contextuellement génèrent des avertissements, de sorte que les fautes d'orthographe et les paramètres inefficaces sont visibles dans le journal PalDefender.

| Configuration | Résultat |
| --- | --- |
| Une entrée contient à la fois `ItemID` et `EXP` | Erreur : une entrée ne peut définir qu'un seul type de récompense. |
| Une entrée de récompense n'a pas de champ d'objet, d'œuf ou de progression | Erreur : PalDefender ne sait pas quoi accorder. |
| `Count: 0`, `Weight: 0` ou `Rolls: 0` | Erreur : ces valeurs doivent être au moins `1`. |
| Une plage omet `Min` ou `Max`, ou contient `Max < Min` | Erreur. |
| `Chance` est en dehors de `0`–`100` | Erreur. |
| Un pool n'a pas de `Entries`, un `Entries` vide array ou une valeur non array | Erreur. |
| `Chance` est placé sur une entrée `OneOf`, `Pick` ou `All` | Avertissement; la chance d’entrée est ignorée. |
| `Rolls` est défini sur `OneOf`, `All` ou `Independent` | Avertissement; `Rolls` est ignoré. |
| `Weight` ou `Unique` est placé en direct `Drops` | Avertissement; utilisez `Chance` pour les dépôts directs. |
| Un champ inconnu tel que `Wieght` est présent | Avertissement; le champ est inutilisé. |

Utilisez un JSON valide sans commentaires ni virgules finales. Consultez les avertissements de chargement même lorsque l'invocation est toujours en cours de chargement : les avertissements identifient généralement un paramètre qui n'a aucun effet.

## Exemple complet

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Arena Anubis",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
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

## Liste de contrôle de validation

1. Testez d'abord le modèle référencé avec `/givemepal_j <template>`.
2. Utilisez `/getpos` pour `X`, `Y` et `Z` ; RCON doit fournir un ID utilisateur à `/getpos`.
3. Utilisez un JSON valide sans commentaires ni virgules finales.
4. Utilisez un seul type de récompense par entrée de récompense.
5. Vérifiez que chaque pool a un `Entries` array non vide et utilise uniquement les champs qui affectent son `Mode` sélectionné.
6. Exécutez `/summon <filename>` et consultez le journal PalDefender pour connaître les erreurs et avertissements de validation précis.
