# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>Deprecated</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>Deprecated</span> legacy endpoint"
    This legacy reward endpoint is deprecated. Prefer the split <span class='pd-badge pd-badge--beta'>Beta</span> reward endpoints: [give progression](./give-progression.md), [give items](./give-items.md), [give pals](./give-pals.md), [give pal templates](./give-paltemplate.md), and [give Pal eggs](./give-paleggs.md).


## Error responses

This endpoint is deprecated and may not be present in current builds. When available, error bodies use the same REST error envelope as the current API.

| HTTP | Error code | When it happens |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | The `Authorization` header is missing, malformed, or does not match a configured bearer token. |
| `403` | `MISSING_PERMISSION` | The token is valid, but it does not include permission for this deprecated route. |
| `400` | `INVALID_JSON` | A request body was supplied, but it could not be parsed as JSON. |
| `400` | `REQUEST_FAILED` | The legacy reward operation failed while validating or applying the request. |
| `500` | `REQUEST_TIMEOUT` | The internal game-thread callback did not complete within 5 seconds. |

## Examples

### Grant EXP and items

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### Grant Pals and eggs

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

??? info "POST `/v1/pdapi/give` — Grant EXP / items / pals / eggs (atomic)"
    ## POST `/v1/pdapi/give`
    ### What it does
    Grants rewards to a target player in a single server-side transaction-like operation:

    - EXP and/or
    - items and/or
    - pals and/or
    - eggs
    depending on the request body.

    ### Core behavior
    This endpoint is intended to behave **atomically**:

    - either everything is granted
    - or nothing is granted

    If any part fails (invalid input, missing inventory space, invalid IDs, etc.), the server should reject the request and not partially apply it.

    ### Why this matters
    Admin tooling must not accidentally:

    - give EXP but not items
    - give some items but fail on later items
    - spawn pals without placing items

    Atomic behavior avoids messy states and “support tickets from hell”.

    ### What it can grant
    Depending on your implementation, the request may include:

    - `EXP` — adds experience
    - `Lifmunks` — adds Lifmunk Effigy points
    - `TechnologyPoints` — adds tech points
    - `AncientTechnologyPoints` — adds ancient tech points
    - `UnlockTechnology` / `Techs[]` — learn technologies
    - `Items[]` — give one or more items with counts
    - `Pals[]` — give pals by ID + level
    - `PalTemplates[]` — import pal templates by filename
    - `PalEggs[]` — eggs by ID + pal ID / template, optionally with level


    ### Error responses

    This endpoint is deprecated and may not be present in current builds. When available, expect the same REST error envelope used by the current API: `INVALID_TOKEN` (`401`) for failed bearer authentication and `MISSING_PERMISSION` (`403`) when the token is authenticated but not allowed to call the route. Request validation failures are returned as JSON error objects; migrate to the split reward endpoints for endpoint-specific error codes.

    ### Examples

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### Validation & common failure cases
    Typical reasons admins hit errors:

    - Inventory space: not enough room for all items → fail the entire request
    - Invalid IDs: unknown `ItemID`, `PalID`, `EggID`, or missing template file → fail
    - Invalid values:
        - negative / zero counts (depending on rules)
        - invalid levels (too low/high, or non-numeric)
        - missing required fields (e.g., no `UserID`)
    - Player not found / not loaded:
        - user ID not known
        - player not currently online (depending on how your server handles offline grants)

    ### Returns
    Error count and error messages. If status is not 200, check `Errors` for how many errors occurred. `Error` contains the detailed list of what failed.
