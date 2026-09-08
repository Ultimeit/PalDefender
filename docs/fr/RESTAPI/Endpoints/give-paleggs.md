# POST /give/paleggs/{player_identifier}



**Point final :** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.PalEggs.Give`

## Objectif

Donne un ou plusieurs œufs Pal au joueur ciblé.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec `PalEggs`, un array de subventions aux œufs. `EggID` est un [`ItemID`](https://paldeck.cc/items). Chaque œuf doit utiliser soit [`PalID`](https://paldeck.cc/pals) soit `PalTemplate`, pas les deux.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | Le corps ne contient pas de `PalEggs` array. |
| `400` | `VALIDATION_FAILED` | Une ou plusieurs subventions d'œufs sont invalides, ne peuvent pas être importées ou ne rentrent pas dans l'inventaire. |

## Exemples

### Donnez un œuf nivelé à un joueur Steam

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### Donner un œuf basé sur un modèle par PlayerUID

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## Scénarios

- Donnez des œufs d'événement sans faire apparaître immédiatement le Pal.
- Utilisez `PalID` pour les œufs simples et `PalTemplate` pour le contenu des œufs personnalisé.
- La demande peut échouer si l'œuf [`ItemID`](https://paldeck.cc/items) n'est pas valide ou si l'inventaire du joueur n'a pas d'espace.
