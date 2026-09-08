# POST /ReloadConfig



**Point final :** `POST /v1/pdapi/ReloadConfig`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Reload.Config`

## Objectif

Recharge la configuration PalDefender sans nécessiter un redémarrage complet du serveur.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON vide en option object.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/reload-config.md"

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

### Recharger la configuration

```http
POST /v1/pdapi/ReloadConfig
```

### Recharger après les changements de jeton

```http
POST /v1/pdapi/ReloadConfig
```

## Scénarios

- Appliquez les modifications aux fichiers de configuration pris en charge.
- Rechargez après la mise à jour de `Banlist.json`, des règles d'importation ou d'autres fichiers PalDefender lisibles à l'exécution.
- Si une modification ne prend pas effet après le rechargement, redémarrez le serveur pendant une fenêtre de maintenance.
