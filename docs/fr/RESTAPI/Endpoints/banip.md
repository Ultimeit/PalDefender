# POST /banip/{ip}



**Point final :** `POST /v1/pdapi/banip/<ip>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Punishments.BanIP`

## Objectif

Interdit une adresse IP et l'enregistre dans `Banlist.json`.

## Paramètres du chemin

- `ip` : Adresse IP à bannir.

## Paramètres de requête

Aucun.

## Corps de la demande

Champs JSON facultatifs : `Reason` string et `UserId` string lorsque le bannissement IP doit être associé à un utilisateur.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/banip.md"

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

## Exemples

### Interdire une IP uniquement

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "Bot traffic"
}
```

### Bannir une IP et attacher un utilisateur GDK

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "Alt account abuse",
    "UserId": "gdk_2533274898765432"
}
```

## Scénarios

- Arrêtez les abus répétés de la même adresse IP après examen par le personnel.
- Associez `UserId` lorsqu'il est connu afin que la liste de bannissement soit plus facile à auditer.
- Utilisez [GET /banlist](banlist.md) avec `ip` pour vérifier l'enregistrement actif.
