# POST /ban/{player_identifier}



**Point final :** `POST /v1/pdapi/ban/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Punishments.Ban`

## Objectif

Bannit un utilisateur et enregistre l'interdiction dans `Banlist.json`. La cible peut être expulsée si elle est actuellement en ligne.

## Paramètres du chemin

- `player_identifier` : `UserId`, `PlayerUID` ou un autre identifiant de joueur pris en charge.

## Paramètres de requête

Aucun.

## Corps de la demande

Champs JSON facultatifs : `Reason` string et `IP` booléens. Définissez `IP` sur `true` uniquement lorsque vous souhaitez également interdire l'adresse IP résolue.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/ban.md"

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
| `400` | `IP_UNAVAILABLE` | `IP` était `true`, mais le serveur n'a pas pu résoudre l'adresse IP de l'utilisateur cible. |

## Exemples

### Bannir un utilisateur Steam

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "Chargeback fraud"
}
```

### Interdire un utilisateur PS5 et son adresse IP résolue

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "Ban evasion",
    "IP": true
}
```

## Scénarios

- Bannir un joueur avant `UserId` après examen de modération.
- Incluez une raison claire afin que le futur personnel puisse comprendre l'entrée de la liste d'interdiction.
- Utilisez [GET /banlist](banlist.md) pour vérifier l'enregistrement actif. Les données liées au bannissement ne sont plus gérées dans `Config.json`.
