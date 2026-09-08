# GET /progression/{player_identifier}



**Point final :** `GET /v1/pdapi/progression/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Progression.Read`

## Objectif

Lit les valeurs de progression du joueur telles que l'EXP, l'état lié au niveau, les totaux de reliques et les totaux de points technologiques.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` | Le joueur cible, le compte, les données de personnage individuel, les données d'enregistrement ou les données technologiques n'ont pas pu être résolus. |
| `500` | `REQUEST_TIMEOUT` | Le rappel du thread de jeu interne ne s'est pas terminé dans les 5 secondes. |

## Exemples

### Lire la progression par ID utilisateur PS5

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### Lire la progression par PlayerUID

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Scénarios

- Confirmez les valeurs actuelles avant d’accorder la progression.
- Vérifiez une action d'assistance après [POST /give/progression](give-progression.md).
- Créez un panneau de présentation des joueurs dans un tableau de bord d'administrateur de confiance.
