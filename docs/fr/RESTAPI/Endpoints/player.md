# GET /player/{player_identifier}



**Point final :** `GET /v1/pdapi/player/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Player.Read`

## Objectif

Renvoie un joueur. L'identifiant peut être un identifiant de joueur pris en charge tel que `UserId` ou `PlayerUID`.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/player.md"

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
| `404` | `PLAYER_NOT_FOUND` | Aucun joueur en ligne ne correspond au `player_identifier` fourni. |
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | Le joueur a été trouvé, mais les données du compte joueur n'ont pas pu être chargées. |

## Exemples

### Recherche par Steam UserID

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### Recherche par PlayerUID

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## Scénarios

- Ouvrez une page de détails sur un joueur après avoir sélectionné une ligne dans `GET /players`.
- Confirmez la cible avant de donner des récompenses ou d'appliquer des punitions.
- Vérifiez si le joueur peut actuellement être résolu par le serveur.
