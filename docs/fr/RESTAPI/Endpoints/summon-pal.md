# POST /summon/pal

**Point final :** `POST /v1/pdapi/summon/pal`
**Auth :** Jeton du porteur
**Autorisation :** `REST.Summon.Pal`

## Objectif

Génère un Pal à des coordonnées cartographiques fixes. La demande doit fournir exactement l’un des `PalID` ou `PalTemplate`.

## Corps de la demande

| Champ | Type | Obligatoire | Descriptif |
| --- | --- | --- | --- |
| `PalID` | string | L'un des | Pal ID d'espèce. Mutuellement exclusif avec `PalTemplate`. |
| `PalTemplate` | string | L'un des | Nom de fichier de `Pals/Templates/` ; utilise le Pal et le niveau du modèle. |
| `X`, `Y`, `Z` | numéro | Oui | Coordonnées de la carte. |
| `Level` | integer | Non | Niveau pour les invocations `PalID` (par défaut `1`). Ignoré pour un modèle. |
| `Uncapturable` | bool | Non | Empêche la capture (par défaut `false`). |
| `DisableAI` | bool | Non | Désactive l'IA normale (`false` par défaut). |
| `DisableDamageMeter` | bool | Non | Désactive le suivi des dommages (par défaut `false`). |
| `DisableStatuses` | array | Non | Noms de statut à supprimer. |

!!! warning "Migration des PV maximum"
    Lorsque `PalTemplate` est utilisé, la valeur `HP` du modèle devient les PV maximum du Pal généré. `HealthMultiplier` et `HPMultiplier` ne sont plus acceptés dans les requêtes ni renvoyés dans les réponses ; supprimez-les des intégrations REST existantes.

## Schéma de réponse

--8<-- "_snippets/restapi/schemas/summon-pal.md"

## Erreurs

Outre les réponses standard `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED` et `REQUEST_TIMEOUT`, cette route peut renvoyer `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED` ou `SUMMON_PAL_FAILED`.

## Exemple

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true
}
```
