# POST /Broadcast



**Point final :** `POST /v1/pdapi/Broadcast`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Messages.Broadcast`

## Objectif

Diffuse un message de discussion sur le serveur.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec un `Message` string requis.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/broadcast.md"

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

## Exemples

### Diffusez un avertissement de redémarrage

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "Restart in 15 minutes."
}
```

## Scénarios

- Annoncer la maintenance programmée.
- Envoyez des messages de démarrage d’événement automatisés.
- Utilisez [POST /Alert](alert.md) lorsque le message doit être une alerte au lieu d'une discussion de diffusion normale.
