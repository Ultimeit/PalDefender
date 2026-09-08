# POST /Alert



**Point final :** `POST /v1/pdapi/Alert`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Messages.Alert`

## Objectif

Envoie un message d'alerte au serveur.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec `Message` string.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/alert.md"

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
| `400` | `VALIDATION_FAILED` | `Message` est manquant, vide ou n'est pas un string. |
| `400` | `BROADCAST_ALERT_FAILED` | Le serveur n'a pas réussi à envoyer le message d'alerte. |

## Exemples

### Envoyer une alerte de redémarrage

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Restart now."
}
```

### Envoyer une alerte multiligne

```http
POST /v1/pdapi/Alert
```

```json
{
    "Message": "Server restart in 5 minutes.\nPlease return to base."
}
```

## Scénarios

- Envoyez des avertissements de serveur hautement prioritaires.
- À utiliser après une diffusion lorsque les joueurs ont besoin d'un dernier avis urgent.
- Gardez les alertes courtes afin qu’elles soient lisibles dans le jeu.
