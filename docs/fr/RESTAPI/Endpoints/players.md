# GET /players



**Point final :** `GET /v1/pdapi/players`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Players.Read`

## Objectif

Répertorie les joueurs connus avec des informations d'identification et de statut. Utilisez-le pour créer des sélecteurs de joueurs pour les outils d'administration.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | Le serveur n'a pas pu accéder au gestionnaire de lecteur Palworld. |

## Exemples

### Liste tous les joueurs connus

```http
GET /v1/pdapi/players
```

### Actualiser un sélecteur de joueur administrateur

```http
GET /v1/pdapi/players
```

## Scénarios

- Créez une liste déroulante de joueurs en ligne et connus.
- Recherchez le `UserId` ou le `PlayerUID` correct avant d'appeler les points de terminaison de récompense, de punition ou d'inventaire.
- Vérifiez qui est en ligne avant d’envoyer un message ou un avertissement de maintenance programmée.

## Connexes

- [GET /player](player.md) pour un joueur.
- [POST /kick](kick.md), [POST /ban](ban.md) et les points de terminaison des récompenses utilisent le même style d'identifiant de joueur.
