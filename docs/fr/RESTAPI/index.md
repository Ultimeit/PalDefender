# PalDefender REST API

Cette section documente le PalDefender REST API intégré (une petite interface HTTP destinée à une utilisation **locale/de confiance**).

- **URL de base par défaut :** `http://127.0.0.1:17993`
- **Auth :** Jeton du porteur (obligatoire sur tous les points de terminaison)
- **Point de terminaison de la version :** `/v1/pdapi/version`

> Note de sécurité : n'exposez **pas** ce port directement à l'Internet public. Si vous avez besoin d'un accès à distance, utilisez un proxy inverse et des contrôles d'accès appropriés.

## Qu'y a-t-il ici
- [Authentification et configuration](authentication.md)
- [Points de terminaison](Endpoints/index.md)
