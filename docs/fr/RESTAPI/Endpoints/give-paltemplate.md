# POST /give/paltemplate/{player_identifier}



**Point final :** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.PalTemplates.Give`

## Objectif

Donne un ou plusieurs Pals à partir des fichiers dans `Pals/Templates/`.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec `PalTemplates`, un array de noms de fichiers de modèles. L'extension `.json` peut être incluse pour plus de clarté.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | Le corps ne contient pas de `PalTemplates` array. |
| `400` | `VALIDATION_FAILED` | Un ou plusieurs noms de fichiers de modèles ne sont pas valides, ne peuvent pas être importés ou ne rentrent pas dans le stockage Pal. |

## Exemples

### Donnez un modèle Pal à un joueur Steam

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### Donner des modèles de récompense de raid à un joueur PS5

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## Scénarios

- À utiliser lorsque les récompenses nécessitent des compétences spécifiques, des passifs, des IV, des âmes, un surnom ou des valeurs d'aptitude au travail.
- Utilisez [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md) pour créer d'abord le modèle.
- Les règles d'importation dans `Pals/ImportRules/` peuvent bloquer ou ajuster les modèles avant qu'ils ne soient accordés.
