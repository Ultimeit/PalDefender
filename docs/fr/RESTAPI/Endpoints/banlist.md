# GET /banlist



**Point final :** `GET /v1/pdapi/banlist`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Banlist.Read`

## Objectif

Lit les enregistrements d'interdiction de la liste des interdictions. Les données liées au bannissement sont stockées dans `Banlist.json`, et non dans `Config.json`.

## Paramètres du chemin

Aucun.

## Paramètres de requête

- `active` : `true`, `false` ou `1` pour filtrer l'état actif.
- `entryType` : Filtrer par type d'entrée d'interdiction.
- `userId` : Filtrer par ID utilisateur.
- `ip` ou `userIP` : Filtrer par adresse IP.
- `issuerType`, `issuerName`, `issuerIP` : filtrer par métadonnées d'émetteur.
- `reason` : Filtrer par texte de raison.
- `q` : Recherche de texte générale.

## Corps de la demande

Aucun corps de requête.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/banlist.md"

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

### Répertorier tous les enregistrements d'interdiction

```http
GET /v1/pdapi/banlist
```

### Rechercher des enregistrements actifs pour un utilisateur Steam

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### Rechercher des enregistrements par IP

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## Scénarios

- Vérifiez si un joueur ou une adresse IP est actuellement banni.
- Recherchez par motif ou par émetteur avant d'annuler le bannissement.
- Créez un tableau de bord de modération qui lit de `Banlist.json` à API.

## Connexes

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md) et [POST /unbanip](unbanip.md).
