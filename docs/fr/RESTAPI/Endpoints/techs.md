# GET /techs/{player_identifier}



**Point final :** `GET /v1/pdapi/techs/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Techs.Read`

## Objectif

Répertorie les informations technologiques d'un joueur. Les identifiants technologiques peuvent être recherchés sur [paldeck.cc/technology](https://paldeck.cc/technology).

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | Le joueur cible, le compte de joueur, les données technologiques ou le tableau technologique n'ont pas pu être résolus. |
| `500` | `REQUEST_TIMEOUT` | Le rappel du thread de jeu interne ne s'est pas terminé dans les 5 secondes. |

## Exemples

### Lire les technologies déverrouillées par UserID

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### Lire les technologies débloquées par PlayerUID

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## Scénarios

- Vérifiez si un joueur possède déjà un [`TechID`](https://paldeck.cc/technology) avant de l'apprendre ou de l'oublier.
- Créez une page d'administration qui sépare les technologies déverrouillées et disponibles.
- Progression de l'audit après les actions de support.
