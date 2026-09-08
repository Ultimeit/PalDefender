# POST /SendPlayerMessage



**Point final :** `POST /v1/pdapi/SendPlayerMessage`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## Objectif

Envoie un message à un ou plusieurs joueurs cibles.

## Paramètres du chemin

Aucun.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec `SendType`, `Message` et soit `UserID` ou `UserIDs`. Les valeurs `SendType` courantes incluent `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant` et `PlayerLogVeryImportant`.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` | Le corps de la requête est vide. |
| `400` | `INVALID_JSON` | Le corps de la demande n'est pas valide JSON. |
| `400` | `VALIDATION_FAILED` | `SendType`, `Message`, `UserID` ou `UserIDs` est manquant, vide, dupliqué ou a un type incorrect. |
| `400` | `PLAYER_NOT_FOUND` | Un ou plusieurs ID utilisateur cible ou UID de joueur sont introuvables. |
| `400` | `SEND_MESSAGE_FAILED` | La validation a réussi, mais le serveur a rejeté l'opération d'envoi du message. |
| `400` | `REQUEST_FAILED` | Le rappel du thread de jeu a levé une exception. |
| `500` | `REQUEST_TIMEOUT` | Le rappel du thread de jeu interne ne s'est pas terminé dans les 5 secondes. |

## Exemples

### Envoyer le chat du joueur à un utilisateur

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "Your shop order has arrived."
}
```

### Envoyer un journal important à des cibles mixtes

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "The event starts in 10 minutes."
}
```

## Scénarios

- Envoyez des avertissements de redémarrage direct aux joueurs sélectionnés.
- Envoyez des réponses d’assistance à partir d’un panneau d’administration.
- Utilisez `UserID` pour une cible et `UserIDs` pour plusieurs cibles, pas les deux.
