# GET /items/{player_identifier}



**Point final :** `GET /v1/pdapi/items/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Items.Read`

## Objectif

Répertorie les objets du joueur cible. Les identifiants d'éléments dans les réponses peuvent être recherchés sur [paldeck.cc/items](https://paldeck.cc/items).

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` | Le joueur cible, l'état du joueur, les données d'inventaire ou le conteneur d'inventaire commun n'ont pas pu être résolus. |
| `500` | `REQUEST_TIMEOUT` | Le rappel du thread de jeu interne ne s'est pas terminé dans les 5 secondes. |

## Exemples

### Lire l'inventaire d'un joueur Steam

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### Lire l'inventaire d'un joueur GDK

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## Scénarios

- Vérifiez l’inventaire avant d’accorder une compensation.
- Confirmez un [`ItemID`](https://paldeck.cc/items) avant d'utiliser [POST /give/items](give-items.md).
- Résoudre les rapports sur les éléments manquants.
