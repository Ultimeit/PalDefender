# GET /guild/{guild_id}



**Point final :** `GET /v1/pdapi/guild/<guild_id>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Guild.Read`

## Objectif

Renvoie une guilde avec des informations détaillées sur les membres et base/camp.

## Paramètres du chemin

- `guild_id` : Identifiant de guilde, généralement copié de [GET /guilds](guilds.md).

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` | Aucune guilde ne correspondait au `guild_id` fourni. |

## Exemples

### Lire la liste des guildes et les camps

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### Lisez une autre guilde par GUID

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## Scénarios

- Enquêtez sur la propriété de la base avant de supprimer une base.
- Examinez les membres de la guilde et les données du camp pour les demandes d'assistance.
- Utilisez soigneusement les identifiants de camp de la réponse avec [POST /deletebase](deletebase.md).
