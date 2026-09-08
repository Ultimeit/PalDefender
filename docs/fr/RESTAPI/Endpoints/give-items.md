# POST /give/items/{player_identifier}



**Point final :** `POST /v1/pdapi/give/items/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Items.Give`

## Objectif

Donne un ou plusieurs objets au joueur cible.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec `Items`, un array d'objets accordés. Chaque entrée nécessite un [`ItemID`](https://paldeck.cc/items) et un `Count` positif.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` | Le corps ne contient pas de `Items` array. |
| `400` | `VALIDATION_FAILED` | Une ou plusieurs subventions d'articles ne sont pas valides, ne sont pas prises en charge, sont trop volumineuses ou ne rentrent pas dans l'inventaire. |
| `500` | `GRANT_FAILED` | La validation a réussi, mais le serveur a échoué lors de l'ajout d'éléments à l'inventaire. |

## Exemples

### Donnez des munitions et un lanceur à un joueur Steam

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### Donnez de la monnaie à un joueur PS5

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## Scénarios

- À utiliser pour les packages de compensation après une restauration.
- À utiliser pour les intégrations de boutique où un service de confiance accorde les articles achetés.
- Validez d'abord le [`ItemID`](https://paldeck.cc/items) ; les noms d’affichage ne sont pas toujours des identifiants valides.
