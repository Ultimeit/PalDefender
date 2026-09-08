# POST /unbanip/{ip}



**Point final :** `POST /v1/pdapi/unbanip/<ip>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Punishments.UnbanIP`

## Objectif

Annule une adresse IP dans `Banlist.json`.

## Paramètres du chemin

- `ip` : adresse IP à débannir.

## Paramètres de requête

Aucun.

## Corps de la demande

Champ JSON facultatif : `Reason` string.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/unbanip.md"

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
| `404` | `BAN_NOT_FOUND` | Le `ip` fourni n'est pas activement interdit. |

## Exemples

### Débannir une IP avec raison

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "Temporary block expired"
}
```

### Annuler le bannissement d'une IP avec la raison par défaut

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## Scénarios

- Supprimez une interdiction IP après enquête.
- À utiliser lorsqu'un joueur est toujours bloqué après une levée de bannissement au niveau de l'utilisateur, car l'enregistrement IP reste actif.
- Utilisez [GET /banlist](banlist.md) avec `ip` pour vérifier le résultat.
