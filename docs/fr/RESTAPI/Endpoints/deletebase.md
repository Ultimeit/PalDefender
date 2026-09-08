# POST /deletebase/{base_camp_id}



**Point final :** `POST /v1/pdapi/deletebase/<base_camp_id>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Base.Delete`

## Objectif

Supprime un base/camp par son ID de camp de base. Il s’agit d’une action administrative destructrice.

## Paramètres du chemin

- `base_camp_id` : identifiant du camp de base, généralement copié à partir des données guild/base.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON vide en option object. Confirmez l'identifiant avant d'envoyer la demande.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | La valeur du chemin `base_camp_id` n'est pas un GUID valide. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | Le serveur n'a pas pu accéder à `UPalBaseCampManager`. |
| `404` | `BASE_CAMP_NOT_FOUND` | Aucun camp de base ne correspond au GUID fourni. |
| `500` | `DELETE_BASE_FAILED` | Le camp de base a été trouvé, mais destruction/cleanup a échoué. |

## Exemples

### Supprimer un camp de base par GUID

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### Supprimer un autre camp de base par GUID

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## Scénarios

- Retirez les bases abandonnées ou cassées après examen par le personnel.
- Utilisez [GET /guilds](guilds.md) et [GET /guild](guild.md) pour identifier le camp correct avant la suppression.
- N'utilisez pas ce point de terminaison pour un nettoyage de routine à moins que votre processus personnel ne vérifie déjà la propriété et les sauvegardes.
