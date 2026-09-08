# POST /forgettech/{player_identifier}



**Point final :** `POST /v1/pdapi/forgettech/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Techs.Forget`

## Objectif

Oublie une, plusieurs ou toutes les technologies pour un joueur.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

`Technology` peut être un seul [`TechID`](https://paldeck.cc/technology), la string `"All"` ou un array de strings [`TechID`](https://paldeck.cc/technology). Ne placez pas `"All"` dans un array.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/forgettech.md"

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

### Oubliez une technologie pour un lecteur GDK

```http
POST /v1/pdapi/forgettech/gdk_2533274812345678
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### Oubliez plusieurs technologies par PlayerUID

```http
POST /v1/pdapi/forgettech/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### Oubliez toutes les technologies pour un joueur Steam

```http
POST /v1/pdapi/forgettech/steam_76561198012345678
```

```json
{
    "Technology": "All"
}
```

## Scénarios

- Supprimer une technologie accordée par erreur.
- Réinitialisez un compte test avec `"All"`.
- Confirmez l'état actuel avec [GET /techs](techs.md) avant et après la demande.
