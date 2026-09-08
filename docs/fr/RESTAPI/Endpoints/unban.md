# POST /unban/{user_id}



**Point final :** `POST /v1/pdapi/unban/<user_id>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Punishments.Unban`

## Objectif

Libère un identifiant utilisateur dans `Banlist.json`.

## Paramètres du chemin

- `user_id` : ID utilisateur à débloquer.

## Paramètres de requête

Aucun.

## Corps de la demande

Champ JSON facultatif : `Reason` string.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/unban.md"

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
| `400` | `VALIDATION_FAILED` | Un champ de requête facultatif a un type JSON incorrect. |
| `404` | `BAN_NOT_FOUND` | Le `user_id` fourni n'est pas activement interdit. |

## Exemples

### Annuler le bannissement d'un utilisateur Steam

```http
POST /v1/pdapi/unban/steam_76561198012345678
```

```json
{
    "Reason": "Appeal accepted"
}
```

### Annuler le bannissement d'un utilisateur PS5 avec une raison par défaut

```http
POST /v1/pdapi/unban/ps5_c481a77e22004b9d
```

```json
{}
```

## Scénarios

- Supprimez une interdiction d'utilisateur après l'approbation de l'appel.
- Conservez une raison pour la piste d’audit.
- Utilisez [GET /banlist](banlist.md) avec `userId` ou `q` pour vérifier le résultat.
