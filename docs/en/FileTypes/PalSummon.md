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
| `DamageTakenMultiplier` | number | `1.0` | Multiplier for damage received; negative values fall back to `1.0`. |
| `DamageDealtMultiplier` | number | `1.0` | Multiplier for damage dealt; negative values fall back to `1.0`. |
| `X`, `Y`, `Z` | number | Required | Map coordinates. Use `/getpos` to obtain them. |
| `DisableStatuses` | array | Empty | Status names to suppress. Invalid names are skipped. |
| `Rewards` | object or array | Empty | Optional rank-specific and default [reward definitions](#damage-meter-and-rewards). The object form is recommended. |

`CapturableAt`, `CapturableAtPercent`, and `capturable_at` are accepted compatibility aliases. `AdditionalEnemyReceiveDamageRate` and `AdditionalEnemyInflictDamageRate` are also accepted, but the names in the table are preferred.

!!! warning "Maximum HP migration"
    The summoned Pal's maximum HP is now taken from `HP` in the referenced PalTemplate. `HealthMultiplier`, `HPMultiplier`, and `AdditionalEnemyMaxHPRate` are no longer supported; remove these fields from existing PalSummon files.

## Damage meter and rewards { #damage-meter-and-rewards }

Rewards are resolved after the summoned Pal dies or is captured. The damage leaderboard is sorted from highest to lowest damage. The result dialog shows the top five, highlights the top three, and also shows the receiving player's own position when that player is outside the top five.

With damage tracking enabled, each participating player is handled as follows:

1. PalDefender looks for a numeric `Rewards` key matching that player's final rank.
2. If that exact rank does not exist, PalDefender uses `Rewards.Default`.
3. If neither exists, that player receives no reward.
4. The selected reward is rolled separately for that player. Two players using the same `Default` definition can therefore receive different random results.

Only participants who are still online and have an available player controller when the encounter finishes can receive ranked rewards. A numbered reward does not include the `Default` reward; it replaces it for that rank.

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

In this example, first place receives both guaranteed drops, second place receives a random amount of EXP, and every other ranked participant independently has a 75% chance to receive 1,000 Money.

Rank keys must be positive whole numbers written as JSON object keys, such as `"1"`, `"2"`, or `"10"`. `"0"`, negative ranks, and arbitrary names are invalid. `Default` is matched case-insensitively.

??? note "Array form"
    `Rewards` may also be an array. Array element 0 is rank 1, element 1 is rank 2, and so on. The array form cannot define `Default`, so the object form is clearer and is recommended.

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### Reward definition structure

Every rank and `Default` contains one reward definition. A definition can contain both:

- `Drops`: entries evaluated directly and independently.
- `Pools`: groups that control how entries are selected.

It may also contain the progression shorthands `EXP`, `TechnologyPoints`, and `AncientTechnologyPoints`. Shorthands are guaranteed and are useful when they do not need their own `Chance`, `Weight`, or `Unique` setting.

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### Reward entry types

Each entry must define exactly one reward type. Do not combine an item, egg, and progression field in the same entry.

| Reward | Required fields | Optional fields | Notes |
| --- | --- | --- | --- |
| Item | `ItemID` | `Count`, `Chance`, `Weight`, `Unique` | `Count` defaults to `1`. |
| Pal egg | `EggID`, `PalTemplate` | `Count`, `Level`, `Chance`, `Weight`, `Unique` | `Count` defaults to `1`; `Level: 0` uses the template's level. |
| Experience | `EXP` | `Chance`, `Weight`, `Unique` | The `EXP` value is the amount or range. |
| Technology points | `TechnologyPoints` | `Chance`, `Weight`, `Unique` | The field value is the amount or range. |
| Ancient technology points | `AncientTechnologyPoints` | `Chance`, `Weight`, `Unique` | The field value is the amount or range. |

`Chance`, `Weight`, and `Unique` are only effective in the contexts described below. A field being accepted by the parser does not mean it affects every distribution mode.

The canonical field names above are recommended. The parser also accepts these aliases:

| Canonical field | Accepted aliases |
| --- | --- |
| `ItemID` | `ItemId`, `ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`, `Num` |
| `EXP` | `Exp`, `Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### Fixed values, ranges, and chances

Amounts can be a fixed whole number or an inclusive range:

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- `Count`, EXP, and technology-point amounts must be whole numbers of at least `1`.
- A range needs both `Min` and `Max`, and `Max` must not be lower than `Min`.
- Text ranges such as `"1-3"` are invalid; use `{ "Min": 1, "Max": 3 }`.
- Egg `Level` may be `0`; this keeps the level from the referenced PalTemplate. A positive level overrides the template level and is capped at level 255 when the egg is granted.
- `Chance` accepts a number or numeric text with an optional `%`, for example `30`, `30.5`, or `"30%"`.
- `Chance: 0` never succeeds, `Chance: 100` always succeeds, and values must stay between `0` and `100`.
- For a chance strictly between 0 and 100, the generated roll must be lower than the configured value. A roll of exactly `30.0` therefore fails a `Chance` of `30`.

### Direct drops

Every entry in `Drops` is evaluated independently. There is no choose-one relationship between neighboring entries. Missing `Chance` means `100`.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

The Money is guaranteed. The ammunition, EXP, and technology points each make their own chance roll. Zero, one, two, or all three optional drops may succeed.

`Weight` and `Unique` do not work in direct `Drops` and produce warnings. Use `Chance` for optional direct drops.

## Loot pools

A pool first rolls its own `Chance`. If the pool fails, none of its entries are considered. If it succeeds, `Mode` decides how the entries are evaluated.

| Pool key | Type | Default | Description |
| --- | --- | --- | --- |
| `Name` | string | Empty | Optional diagnostic label. It does not affect selection. |
| `Mode` | string | `OneOf` | `OneOf`, `Pick`, `All`, or `Independent`. Matching is case-insensitive. |
| `Chance` | number or percentage text | `100` | Chance that the entire pool activates. |
| `Rolls` | whole number | `1` | Number of selections in `Pick`; ignored by the other modes. |
| `Unique` | bool | `true` | Default repeat policy for `Pick`; an entry may override it. |
| `Entries` | array | Required | Non-empty list of reward entries. |

`One` is accepted as an alias for `OneOf`, and `PickN` as an alias for `Pick`, but the canonical mode names are recommended.

| Mode | How many entries can be granted? | Uses `Weight`? | Uses entry `Chance`? | Uses `Rolls` / `Unique`? |
| --- | --- | --- | --- | --- |
| `OneOf` | Exactly one if the pool succeeds | Yes | No | No |
| `Pick` | Up to `Rolls` selections | Yes | No | Yes |
| `All` | Every entry once if the pool succeeds | No | No | No |
| `Independent` | Zero through all entries | No | Yes | No |

All four modes still use the pool-level `Chance`. Multiple pools in one reward definition are processed independently, and their results are added to direct `Drops`.

### `OneOf`: one weighted result

`OneOf` is the default mode. If its pool-level chance succeeds, exactly one entry is selected. The probability of an entry is its `Weight` divided by the sum of all entry weights.

```json
{
    "Pools": [
        {
            "Name": "Equipment jackpot",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

The weights total 20. Conditional on the pool succeeding, the four entries have probabilities of 35%, 35%, 25%, and 5%. Because the pool itself activates only 35% of the time, the egg's absolute chance is `35% × 5% = 1.75%`.

- Missing `Weight` defaults to `1`.
- `Weight` must be a whole number of at least `1`; remove an entry instead of assigning weight `0`.
- `Rolls` is ignored and produces a warning because `OneOf` always selects once.
- Entry-level `Chance` is ignored and produces a warning. Use `Weight` to control the relative selection probability.
- `Unique` has no practical effect because only one entry is selected.

### `Pick`: multiple weighted results without repeats

`Pick` repeats weighted selection `Rolls` times. With the default `Unique: true`, a selected entry is removed before the next selection and cannot be selected again. Weights are recalculated from the remaining entries after each selection.

```json
{
    "Pools": [
        {
            "Name": "Choose two different rewards",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

This grants two different entries. If `Rolls` is greater than the number of available unique entries, selection stops when no entries remain; it is not an error.

### `Pick`: allowing repeated results

Set the pool's `Unique` to `false` to keep selected entries available for later rolls. Repeated grants of the same item are merged before delivery.

```json
{
    "Pools": [
        {
            "Name": "Three supply rolls",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

All three rolls may select Money, all may select ammunition, or the results may be mixed. For example, selecting Money twice produces one Money grant of 10,000 rather than two separate grants.

### `Pick`: overriding `Unique` per entry

An entry-level `Unique` overrides the pool default only for that entry. This allows repeatable common rewards and one-time jackpot rewards in the same pool.

```json
{
    "Pools": [
        {
            "Name": "Repeatable currency with unique jackpots",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

Money remains in the candidate list after being selected because its entry says `Unique: false`. The armor and helmet inherit `Unique: true` from the pool and are removed after selection. The reverse is also valid: a pool can use `Unique: false` while a particular entry uses `Unique: true`.

### `All`: grant every entry

`All` grants every entry exactly once when the pool-level `Chance` succeeds.

```json
{
    "Pools": [
        {
            "Name": "Complete reward bundle",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`Weight`, entry-level `Chance`, and `Unique` do not affect `All`. `Rolls` is ignored and produces a warning. To make the entire bundle optional, set the pool's `Chance`; to make individual entries optional, use `Independent` or direct `Drops` instead.

### `Independent`: roll every entry separately

`Independent` checks every entry and uses each entry's own `Chance`. It can grant no entries, one entry, several entries, or all entries.

```json
{
    "Pools": [
        {
            "Name": "Independent bonus rolls",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

First, the pool has an 80% chance to activate. If it activates, Money is guaranteed because its entry omits `Chance`; the other three entries roll 50%, 10%, and 5% independently.

- Missing entry `Chance` defaults to `100`.
- `Weight` and `Unique` do not affect this mode.
- `Rolls` is ignored and produces a warning because every entry is checked once.

### Combining direct drops and multiple pools

Use multiple pools when one recipient should receive several independently structured reward layers.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "One equipment item",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "Two supply rolls",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "Rare independent bonuses",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

The direct Money and EXP always apply. The first pool adds one equipment item, the second makes two weighted supply selections with replacement, and the third makes two independent bonus rolls. A player can receive results from every pool because pools do not compete with one another.

### Pal egg rewards

An egg needs both `EggID` and `PalTemplate`. The template is loaded from `Pals/Templates/`, and `.json` may be omitted. `Count` controls how many eggs are granted. `Level: 0` or an omitted level keeps the template level; a positive fixed value or range overrides it.

```json
{
    "Pools": [
        {
            "Name": "One random egg reward",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

If an egg template cannot be imported when the reward is granted, PalDefender logs an error and skips that egg reward.

### Merging repeated results

Results from direct drops and all pools are combined before delivery:

- Items with the same `ItemID` are merged by adding their counts.
- Eggs merge only when `EggID`, `PalTemplate`, and the rolled `Level` are all identical.
- EXP, technology points, and ancient technology points are added together.
- Grantable item and technology-point totals are clamped to the signed 32-bit maximum (`2,147,483,647`).

This means repeated `Pick` results do not create duplicate inventory rows in the reward request. Eggs with different rolled levels remain separate rewards.

### `DisableDamageMeter` distribution

When `DisableDamageMeter` is `true`, PalDefender does not build a damage leaderboard and does not use numeric rank rewards. Instead, it rolls `Rewards.Default` separately for **every player who is online when the encounter finishes**, including players who did not damage the summoned Pal.

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

The Money is granted to every online player. Each player independently rolls the two optional point rewards. If `Default` is missing or empty, nobody receives a reward in this mode and PalDefender writes a warning to the log.

### Invalid and ignored combinations

Invalid reward data prevents the PalSummon file from loading. Unknown or contextually ignored fields produce warnings so spelling mistakes and ineffective settings are visible in the PalDefender log.

| Configuration | Result |
| --- | --- |
| One entry contains both `ItemID` and `EXP` | Error: an entry may define only one reward type. |
| A reward entry has no item, egg, or progression field | Error: PalDefender does not know what to grant. |
| `Count: 0`, `Weight: 0`, or `Rolls: 0` | Error: these values must be at least `1`. |
| A range omits `Min` or `Max`, or has `Max < Min` | Error. |
| `Chance` is outside `0`–`100` | Error. |
| A pool has no `Entries`, an empty `Entries` array, or a non-array value | Error. |
| `Chance` is placed on a `OneOf`, `Pick`, or `All` entry | Warning; the entry chance is ignored. |
| `Rolls` is set on `OneOf`, `All`, or `Independent` | Warning; `Rolls` is ignored. |
| `Weight` or `Unique` is placed in direct `Drops` | Warning; use `Chance` for direct drops. |
| An unknown field such as `Wieght` is present | Warning; the field is unused. |

Use valid JSON without comments or trailing commas. Review load warnings even when the summon still loads: warnings usually identify a setting that has no effect.

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
4. Use only one reward type per reward entry.
5. Check that each pool has a non-empty `Entries` array and only uses fields that affect its selected `Mode`.
6. Run `/summon <filename>` and check the PalDefender log for precise validation errors and warnings.
