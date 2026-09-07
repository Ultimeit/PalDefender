# 📄 `PalSummon.json`

A PalSummon file defines a fixed-location encounter launched with `/summon <filename>`. Store files in `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/` and referenced PalTemplates in `Pals/Templates/`.

!!! tip "ID lookup"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) for `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) for passives, and [paldeck.cc/skills](https://paldeck.cc/skills) for skill IDs used by the referenced template.

## Encounter keys

| Key | Type | Default | Description |
| --- | --- | --- | --- |
| `PalTemplate` | string | Required | Filename of a template in `Pals/Templates/`; `.json` may be omitted. |
| `BossBattleName` | string | Pal ID | Display name used in announcements, logs, webhooks, and damage results. |
| `Uncapturable` | bool | `false` | Prevents the summoned Pal from ever being captured. |
| `CapturableAtHealthPercent` | number | `15` | If capturable, enables capture only at this HP percentage or lower (`0`–`100`). Ignored when `Uncapturable` is `true`. |
| `DisableAI` | bool | `false` | Disables normal AI. Some passive behavior, such as dodging, may still occur. |
| `DisableDamageMeter` | bool | `false` | Disables tracking, the result dialog, and rank rewards. The `Default` reward is instead granted to all online players. |
| `SpawnScale` | number | `1.0` | Visual/physical size multiplier; non-positive values fall back to `1.0`. |
| `HealthMultiplier` | number | `1.0` | Maximum-health multiplier; must be finite and greater than zero. |
| `DamageTakenMultiplier` | number | `1.0` | Multiplier for damage received; negative values fall back to `1.0`. |
| `DamageDealtMultiplier` | number | `1.0` | Multiplier for damage dealt; negative values fall back to `1.0`. |
| `X`, `Y`, `Z` | number | Required | Map coordinates. Use `/getpos` to obtain them. |
| `DisableStatuses` | array | Empty | Status names to suppress. Invalid names are skipped. |
| `Rewards` | object | Empty | Optional rank-specific and default [reward definitions](#damage-meter-and-rewards). |

`CapturableAt`, `CapturableAtPercent`, and `capturable_at` are accepted compatibility aliases. `HPMultiplier`, `AdditionalEnemyMaxHPRate`, `AdditionalEnemyReceiveDamageRate`, and `AdditionalEnemyInflictDamageRate` are also accepted, but the names in the table are preferred.

## Damage meter and rewards

The result dialog shows the five highest damage dealers, highlights the top three, and always includes the receiving player's own position. A reward object can contain fixed `Drops` and randomized `Pools`.

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

Numeric keys are damage-meter positions. `Default` applies to positions without a dedicated rank reward. When `DisableDamageMeter` is `true`, only `Default` is used and every online player receives it.

For simple progression rewards, `EXP`, `TechnologyPoints`, or `AncientTechnologyPoints` may also be placed directly inside a rank/default object; using `Drops` is useful when combining them with items and eggs.

### Reward entries

Each entry must define exactly one reward type:

| Reward | Required fields | Optional fields |
| --- | --- | --- |
| Item | `ItemID` | `Count` (default `1`) |
| Pal egg | `EggID`, `PalTemplate` | `Count` (default `1`), `Level` (template level when `0`) |
| Experience | `EXP` | — |
| Technology points | `TechnologyPoints` | — |
| Ancient technology points | `AncientTechnologyPoints` | — |

Amounts may be a fixed whole number or `{ "Min": 1, "Max": 3 }`. Direct `Drops` may specify `Chance` from `0` to `100`. Pool entries use `Weight` for weighted modes, `Chance` for `Independent`, and may override `Unique`.

### Loot pools

| Pool key | Default | Description |
| --- | --- | --- |
| `Name` | Empty | Optional label used for diagnostics. |
| `Mode` | `OneOf` | `OneOf`, `Pick`, `All`, or `Independent`. |
| `Chance` | `100` | Chance that the entire pool activates. |
| `Rolls` | `1` | Selections made by `Pick`. |
| `Unique` | `true` | Prevents duplicate selections in `Pick`; an entry can override it. |
| `Entries` | Required | Reward-entry array. |

- `OneOf` selects one entry using `Weight`.
- `Pick` makes `Rolls` weighted selections.
- `All` grants every entry.
- `Independent` rolls every entry's `Chance` separately.

```json
"Pools": [
    {
        "Name": "Rare drop",
        "Mode": "OneOf",
        "Chance": 25,
        "Entries": [
            { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 4 },
            { "EggID": "PalEgg_Dragon_05", "PalTemplate": "RaidReward.json", "Level": 50, "Weight": 1 }
        ]
    }
]
```

## Complete example

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Arena Anubis",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "HealthMultiplier": 8.0,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "Winner bonus",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## Validation checklist

1. Test the referenced template first with `/givemepal_j <template>`.
2. Use `/getpos` for `X`, `Y`, and `Z`; RCON must provide a UserId to `/getpos`.
3. Use valid JSON without comments or trailing commas.
4. Use only one reward type per reward row.
6. Run `/summon <filename>` and check the PalDefender log for precise validation errors.
