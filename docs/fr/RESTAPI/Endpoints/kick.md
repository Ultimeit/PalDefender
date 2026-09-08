# POST /kick/{player_identifier}



**Point final :** `POST /v1/pdapi/kick/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Punishments.Kick`

## Objectif

Expulse un joueur en ligne sans créer d'enregistrement d'interdiction.

## Paramètres du chemin

- `player_identifier` : `UserId`, `PlayerUID` ou un autre identifiant de joueur pris en charge.

## Paramètres de requête

Aucun.

## Corps de la demande

Champ JSON facultatif : `Reason` string.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` | Le joueur ciblé n'est pas en ligne ou n'a pas pu être trouvé. |

## Exemples

### Kick un joueur GDK avec raison

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "AFK in event area"
}
```

### Expulser un joueur Steam avec une raison par défaut

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## Scénarios

- Supprimer un joueur avant la maintenance.
- Expulsez un joueur bloqué pour qu'il puisse se reconnecter.
- Utilisez plutôt [POST /ban](ban.md) lorsque le joueur ne doit pas être autorisé à revenir.
