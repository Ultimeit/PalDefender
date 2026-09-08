# POST /give/pals/{player_identifier}



**Point final :** `POST /v1/pdapi/give/pals/<player_identifier>`

**Auth :** Jeton du porteur

**Autorisation :** `REST.Pals.Give`

## Objectif

Donne un ou plusieurs Pals par ID et niveau.

## Paramètres du chemin

- `player_identifier` : `UserId` ou `PlayerUID` pour le joueur cible.

## Paramètres de requête

Aucun.

## Corps de la demande

JSON object avec `Pals`, un array sur Pal subventions. Chaque entrée nécessite un [`PalID`](https://paldeck.cc/pals) et un `Level` positif.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` | Le corps ne contient pas de `Pals` array. |
| `400` | `VALIDATION_FAILED` | Une ou plusieurs subventions Pal ne sont pas valides, ou le joueur ne dispose pas d'un espace de stockage Pal insuffisant. |

## Exemples

### Donnez un starter Pal à un joueur GDK

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### Donner l'événement Pals par PlayerUID

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## Scénarios

- Offrez des récompenses simples Pal sans conserver de fichier modèle.
- À utiliser pour les scripts de récompense aléatoires qui varient uniquement de `PalID` et `Level`.
- La demande peut échouer si le lecteur est introuvable, si le [`PalID`](https://paldeck.cc/pals) n'est pas valide ou s'il n'y a pas suffisamment d'espace de stockage Pal.
