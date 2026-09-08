# Authentification et configuration

## Activation du API

1. Ouvert : `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Réglez `"Enabled"` sur `true`
3. Redémarrez le serveur.

Au démarrage, vous devriez voir des journaux similaires à :
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Loaded 1 Bearer token.
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Port

- **Port par défaut :** `17993`

**Ne l'exposez pas publiquement.** Si vous souhaitez accéder à l'API depuis l'extérieur de votre réseau local ou de votre machine, placez-la derrière un **proxy inverse** (nginx/Caddy/Traefik) et terminez-y TLS. Conservez l'API REST de PalDefender liée à localhost ou à une interface privée.

## Jetons

- Démarrez le serveur une fois pour générer un exemple de jeton.
- Chaque fichier `.json` à l'intérieur de `Win64/PalDefender/RESTAPI/Tokens/` est traité comme un fichier de jeton valide. (La seule exception est le fichier `TokenExample.json` !)
- Créez **un jeton par person/service**.. Les jetons sont des mots de passe.

Exemple de fichier de jeton :

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

    `Permissions` peut être un string ou un array de chaînes. Utilisez des autorisations plus restreintes pour les tableaux de bord publics ou les automatisations qui ne devraient pas avoir un accès administrateur complet.

## En-têtes
Envoyez le jeton via l'en-tête d'autorisation standard :
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Exemple Python
```py
import requests

base_url = "http://127.0.0.1:17993"
# do not do this. Never store the token in any code. use smth like .env! This is only for demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
