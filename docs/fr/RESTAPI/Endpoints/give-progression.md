# POST /give/progression/{player_identifier}



**Point final :** `POST /v1/pdapi/give/progression/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Progression.Give`

## Objectif

Accorde des valeurs de progression à un joueur.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec au moins une subvention prise en charge : positif integer `EXP`, positif integer `TechnologyPoints`, positif integer `AncientTechnologyPoints`, ou `Relics` en tant que object non vide saisi par type de relique avec montants integer positifs.


Types de reliques pris en charge : `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/give-progression.md"

## Réponses aux erreurs

Les corps d'erreur utilisent cette forme :

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP | Code d'erreur | Quand ça arrive |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | L'en-tête `Authorization` est manquant, mal formé ou ne correspond pas à un jeton de support configuré. |
| `403` | `MISSING_PERMISSION` | Le jeton est valide, mais il n'inclut pas cette autorisation de point de terminaison. |
| `400` | `INVALID_JSON` | Un corps de requête a été fourni, mais il n'a pas pu être analysé comme JSON. |
| `400` | `REQUEST_FAILED` | Le rappel du thread de jeu a généré une exception ou un résolveur player/resource partagé a échoué. |
| `500` | `REQUEST_TIMEOUT` | Le rappel du thread de jeu interne ne s'est pas terminé dans les 5 secondes. |
| `400` | `INVALID_REQUEST` | Le corps n’inclut aucun des éléments `EXP`, `Relics`, `TechnologyPoints` ou `AncientTechnologyPoints`. |
| `400` | `VALIDATION_FAILED` | Une valeur de progression fournie est manquante, les éléments internes de progression non integer, non positifs ou requis ne sont pas disponibles. |

## Exemples

### Donnez de l'EXP à un joueur GDK

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### Donnez des points et des reliques par PlayerUID

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## Scénarios

- Compensez les joueurs après une annulation de sauvegarde.
- Ajoutez des points technologiques sans débloquer une technologie spécifique.
- Utilisez plutôt [POST /learntech](learntech.md) lorsque vous souhaitez débloquer un [`TechID`](https://paldeck.cc/technology) spécifique.
