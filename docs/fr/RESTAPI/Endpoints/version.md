# GET /version



**Point final :** `GET /v1/pdapi/version`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Version.Read`

## Objectif

Utilisez ce point de terminaison comme vérification de l’état et vérification de la version des outils, des tableaux de bord et des scripts.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/version.md"

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

## Exemples

### Vérification de l'état de santé et des versions

```http
GET /v1/pdapi/version
```

## Scénarios

- Utilisez-le après avoir configuré le jeton REST API pour confirmer que l'authentification fonctionne.
- Utilisez-le avant d'appeler les points de terminaison si votre outil nécessite une version minimale de PalDefender.
- Utilisez-le pour la surveillance, car il s'agit de la plus petite requête en lecture seule.
