# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>Deprecated</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>Deprecated</span> ancien point de terminaison"
    Cet ancien point de terminaison de récompense est obsolète. Préférez les points de terminaison de récompense fractionnée : [donner une progression](./give-progression.md), [donner des éléments](./give-items.md), [donner pals](./give-pals.md), [donner pal modèles](./give-paltemplate.md) et [donner Pal œufs](./give-paleggs.md).


## Schéma de réponse

--8<-- "_snippets/restapi/schemas/give_deprecated.md"

## Réponses aux erreurs

Ce point de terminaison est obsolète et peut ne pas être présent dans les versions actuelles. Lorsqu'ils sont disponibles, les corps d'erreur utilisent la même enveloppe d'erreur REST que le API actuel.

| HTTP | Code d'erreur | Quand ça arrive |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | L'en-tête `Authorization` est manquant, mal formé ou ne correspond pas à un jeton de support configuré. |
| `403` | `MISSING_PERMISSION` | Le jeton est valide, mais il n'inclut pas l'autorisation pour cette route obsolète. |
| `400` | `INVALID_JSON` | Un corps de requête a été fourni, mais il n'a pas pu être analysé comme JSON. |
| `400` | `REQUEST_FAILED` | L’opération de récompense héritée a échoué lors de la validation ou de l’application de la demande. |
| `500` | `REQUEST_TIMEOUT` | Le rappel du thread de jeu interne ne s'est pas terminé dans les 5 secondes. |

## Exemples

### Accorder de l'EXP et des objets

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### Accordez Pals et des œufs

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

??? info "POST `/v1/pdapi/give` — Accorder de l'EXP/objets/pals/œufs (atomique)"
    ## POST `/v1/pdapi/give`
    ### Ce que ça fait
    Accorde des récompenses à un joueur cible dans une seule opération de type transaction côté serveur :

    - EXP and/or
    - articles and/or
    - pals and/or
    - oeufs
    en fonction du corps de la demande.

    ### Comportement de base
    Ce point de terminaison est destiné à se comporter de manière **atomique** :

    - soit tout est acquis
    - ou rien n'est accordé

    Si une partie échoue (entrée invalide, espace d'inventaire manquant, identifiants invalides, etc.), le serveur doit rejeter la demande et ne pas l'appliquer partiellement.

    ### Pourquoi c'est important
    Les outils d'administration ne doivent pas accidentellement :

    - donne de l'EXP mais pas des objets
    - donner certains éléments mais échouer sur les éléments ultérieurs
    - générer pals sans placer d'objets

    Le comportement atomique évite les états désordonnés et les « tickets de support de l’enfer ».

    ### Ce qu'il peut accorder
    En fonction de votre implémentation, la demande peut inclure :

    - `EXP` — ajoute de l'expérience
    - `Relics` — ajoute des points de relique classés par type de relique
    - `TechnologyPoints` — ajoute des points techniques
    - `AncientTechnologyPoints` — ajoute d'anciens points technologiques
    - `UnlockTechnology` / `Techs[]` — apprendre les technologies
    - `Items[]` — donne un ou plusieurs éléments avec des comptes
    - `Pals[]` — donne pals par ID + niveau
    - `PalTemplates[]` — importer les modèles pal par nom de fichier
    - `PalEggs[]` — œufs par ID + pal ID/modèle, éventuellement avec niveau


    ### Réponses aux erreurs

    Ce point de terminaison est obsolète et peut ne pas être présent dans les versions actuelles. Lorsqu'elle est disponible, attendez-vous à la même enveloppe d'erreur REST utilisée par le API actuel : `INVALID_TOKEN` (`401`) pour l'échec de l'authentification du porteur et `MISSING_PERMISSION` (`403`) lorsque le jeton est authentifié mais n'est pas autorisé à appeler la route. Les échecs de validation des demandes sont renvoyés sous forme d’objets d’erreur JSON ; migrez vers les points de terminaison de récompense fractionnée pour les codes d’erreur spécifiques aux points de terminaison.

    ### Exemples

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### Validation et cas d'échec courants
    Raisons typiques pour lesquelles les administrateurs génèrent des erreurs :

    - Espace d'inventaire : pas assez de place pour tous les articles → échouer la totalité de la demande
    - ID invalides : `ItemID`, `PalID`, `EggID` inconnu ou fichier modèle manquant → échec
    - Valeurs invalides :
        - comptes négatifs / nuls (selon les règles)
        - niveaux non valides (trop low/high ou non numériques)
        - Champs obligatoires manquants (par exemple, non `UserID`)
    - Lecteur introuvable / non chargé :
        - ID utilisateur inconnu
        - joueur qui n'est pas actuellement en ligne (selon la façon dont votre serveur gère les subventions hors ligne)

    ### Retours
    Nombre d'erreurs et messages d'erreur. Si l'état n'est pas 200, vérifiez `Errors` pour connaître le nombre d'erreurs survenues. `Error` contient la liste détaillée de ce qui a échoué.
