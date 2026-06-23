# POST /give/paltemplate/{player_identifier}

<span class='pd-badge pd-badge--beta'>Beta</span>

**Endpoint:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**Auth:** Bearer token

**Permission:** `REST.PalTemplates.Give`

## Purpose

Gives one or more Pals from files in `Pals/Templates/`.

## Path parameters

- `player_identifier`: `UserId` or `PlayerUID` for the target player.

## Query parameters

None.

## Request body

JSON object with `PalTemplates`, an array of template filenames. The `.json` extension may be included for clarity.

## Error responses

Error bodies use this shape:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP | Error code | When it happens |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | The `Authorization` header is missing, malformed, or does not match a configured bearer token. |
| `403` | `MISSING_PERMISSION` | The token is valid, but it does not include this endpoint permission. |
| `400` | `INVALID_JSON` | A request body was supplied, but it could not be parsed as JSON. |
| `400` | `REQUEST_FAILED` | The game-thread callback threw an exception, or a shared player/resource resolver failed. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |
| `400` | `INVALID_REQUEST` | The body does not contain a `PalTemplates` array. |
| `400` | `VALIDATION_FAILED` | One or more template filenames are invalid, cannot be imported, or do not fit in Pal storage. |

## Examples

### Give one template Pal to a Steam player

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### Give raid reward templates to a PS5 player

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## Scenarios

- Use when rewards need specific skills, passives, IVs, souls, nickname, or work suitability values.
- Use [FileTypes/PalTemplates](../../FileTypes/PalTemplate.md) to create the template first.
- Import rules in `Pals/ImportRules/` can block or adjust templates before they are granted.
