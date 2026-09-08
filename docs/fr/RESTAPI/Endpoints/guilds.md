# GET /guilds



**Point final :** `GET /v1/pdapi/guilds`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Guilds.Read`

## Objectif

Répertorie les guildes connues avec des informations récapitulatives. Utilisez ce point de terminaison pour découvrir les identifiants de guilde avant de demander une guilde spécifique.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/guilds.md"

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

## Exemples

### Lister toutes les guildes

```http
GET /v1/pdapi/guilds
```

### Actualiser les données du tableau de bord de guilde

```http
GET /v1/pdapi/guilds
```

## Scénarios

- Créez un sélecteur de guilde dans un panneau d'administration.
- Recherchez le `guild_id` pour [GET /guild](guild.md).
- Auditez le nombre de bases, le nombre de membres et la propriété de la guilde en un coup d'œil.
