# POST /learntech/{player_identifier}



**Point final :** `POST /v1/pdapi/learntech/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Techs.Learn`

## Objectif

Apprend une, plusieurs ou toutes les technologies pour un joueur.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

`Technology` peut être un seul [`TechID`](https://paldeck.cc/technology), la string `"All"` ou un array de strings [`TechID`](https://paldeck.cc/technology). Ne placez pas `"All"` dans un array.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology` est manquant ou il ne s'agit pas d'un string/array au format attendu. |
| `400` | `VALIDATION_FAILED` | Le `Technology` array contient un string non-`All` ou un identifiant technologique non valide. |

## Exemples

### Apprenez une technologie pour un joueur Steam

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Apprenez plusieurs technologies pour un lecteur PS5

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Apprenez toutes les technologies par PlayerUID

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## Scénarios

- Débloquez une recette manquante pour obtenir de l'aide.
- Débloquez toutes les technologies pour les comptes de test.
- Validez les ID de technologie sur [paldeck.cc/technology](https://paldeck.cc/technology) avant d'envoyer la demande.
