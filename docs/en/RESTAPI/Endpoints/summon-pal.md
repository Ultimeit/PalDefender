# POST /summon/pal

**Endpoint:** `POST /v1/pdapi/summon/pal`  
**Auth:** Bearer token  
**Permission:** `REST.Summon.Pal`

## Purpose

Spawns a Pal at fixed map coordinates. The request must provide exactly one of `PalID` or `PalTemplate`.

## Request body

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `PalID` | string | One of | Pal species ID. Mutually exclusive with `PalTemplate`. |
| `PalTemplate` | string | One of | Filename from `Pals/Templates/`; uses the template's Pal and level. |
| `X`, `Y`, `Z` | number | Yes | Map coordinates. |
| `Level` | integer | No | Level for `PalID` summons (default `1`). Ignored for a template. |
| `Uncapturable` | bool | No | Prevents capture (default `false`). |
| `DisableAI` | bool | No | Disables normal AI (default `false`). |
| `DisableDamageMeter` | bool | No | Disables damage tracking (default `false`). |
| `HealthMultiplier` | number | No | Positive health multiplier (default `1.0`). `HPMultiplier` is accepted as an alias. |
| `DisableStatuses` | array | No | Status names to suppress. |

## Response schema

--8<-- "_snippets/restapi/schemas/summon-pal.md"

## Errors

Alongside standard `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED`, and `REQUEST_TIMEOUT` responses, this route may return `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED`, or `SUMMON_PAL_FAILED`.

## Example

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
    "Uncapturable": true,
    "HealthMultiplier": 5.0
}
```
