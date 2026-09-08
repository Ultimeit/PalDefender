# GET /pals/{player_identifier}



**Point final :** `GET /v1/pdapi/pals/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Pals.Read`

## Objectif

Répertorie le Pals du joueur cible. Les identifiants Pal dans les réponses peuvent être recherchés sur [paldeck.cc/pals](https://paldeck.cc/pals).

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/pals.md"

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
| `404` | `PLAYER_STATE_NOT_FOUND` | Le lecteur existe, mais son `APalPlayerState` n'était pas disponible. |

## Exemples

### Lisez Pals pour un lecteur PS5

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### Lire Pals par PlayerUID

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## Scénarios

- Examinez un joueur avant les actions de support.
- Confirmez qu'une récompense Pal est arrivée après avoir utilisé [POST /give/pals](give-pals.md) ou [POST /give/paltemplate](give-paltemplate.md).
- Enquêter sur les rapports concernant des Pals manquants ou inattendus.
