# 📄 `Pals/ImportRules/*.json`

!!! note "<span class='pd-badge pd-badge--beta'>Beta</span>"
    This page is new <span class='pd-badge pd-badge--beta'>Beta</span> documentation for Pal import rule files. It only describes public configuration behavior.

Pal import rules control which `PalTemplate.json` files are allowed, blocked, or adjusted when imported by commands or API actions.

!!! tip "<span class='pd-badge pd-badge--beta'>Beta</span> ID lookup"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) for `AllowedPalIDs`, `BannedPalIDs`, and per-Pal rule filenames. Use [paldeck.cc/passives](https://paldeck.cc/passives) for `DisallowedPassives`.

## File locations

| File | Purpose |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | Global import rules for all Pal templates. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | Optional per-Pal override. Search the [`PalID`](https://paldeck.cc/pals) on Paldeck, then use that exact ID as the filename. Example: `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | Example file generated for reference. It is not a real Pal rule until copied and renamed. |

## Keys

| Key | Type | Description |
| --- | ---- | ----------- |
| `PalSelectionMode` | string | `Default.json` only. `AllowAllExceptBanned` allows every Pal except `BannedPalIDs`. `AllowOnlyListed` allows only `AllowedPalIDs`. |
| `AllowedPalIDs` | array | `Default.json` only. [`PalID`](https://paldeck.cc/pals) values allowed when `PalSelectionMode` is `AllowOnlyListed`. |
| `BannedPalIDs` | array | `Default.json` only. [`PalID`](https://paldeck.cc/pals) values that are always denied. |
| `MaxValueLimitAction` | string | `BlockImport` denies templates above configured limits. `ClampToMaxValues` lowers values to the configured limits. |
| `DisallowedPassivesAction` | string | `BlockImport` denies templates with listed passives. `RemoveFromPal` removes listed passives before import. |
| `DisallowedPassives` | array | [`PassiveID`](https://paldeck.cc/passives) values affected by `DisallowedPassivesAction`. |
| `Disabled` | bool | If `true`, disables import checks for the matching rule set. |
| `BanIfPalIsImpossible` | bool | If `true`, PalDefender can punish impossible Pal imports according to server settings. |
| `AllowGenderNone` | bool | If `false`, templates using `Gender: "None"` can be rejected by import checks. |
| `MaxLevel` | int | Highest allowed Pal level for imported templates. |
| `MaxRank` | int | Highest allowed partner skill rank for imported templates. |
| `PalSouls` | object | Maximum allowed Pal soul values: `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | object | Maximum allowed IV values: `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## <span class='pd-badge pd-badge--beta'>Beta</span> instruction set

1. Start with `Default.json`. Use it for server-wide policy.
2. Use per-Pal files only when one Pal needs different limits.
3. Per-Pal files must be named with the Pal ID, for example `Anubis.json`.
4. Do not put `PalSelectionMode`, `AllowedPalIDs`, or `BannedPalIDs` in per-Pal files. Those belong in `Default.json`.
5. Use `BlockImport` if you want strict moderation.
6. Use `ClampToMaxValues` if you prefer to accept templates but reduce over-limit values.
7. Use `RemoveFromPal` for passives if you prefer automatic cleanup over a failed import.
8. Keep IDs exact and validate JSON before uploading.

## <span class='pd-badge pd-badge--beta'>Beta</span> setup walkthrough

1. Open or create `Pals/ImportRules/Default.json`.
2. Decide the global Pal policy:
   - Use `AllowAllExceptBanned` when most Pals are allowed and you only want to block a few.
   - Use `AllowOnlyListed` when imports should be limited to a curated list.
3. Decide the moderation style:
   - Use `BlockImport` for strict servers where invalid templates should fail.
   - Use `ClampToMaxValues` when you want to accept templates but reduce over-limit levels, ranks, souls, or IVs.
   - Use `RemoveFromPal` for passives when you want to strip unwanted passives instead of rejecting the entire template.
4. Add disallowed passives from [paldeck.cc/passives](https://paldeck.cc/passives).
5. Add banned or allowed Pals from [paldeck.cc/pals](https://paldeck.cc/pals).
6. Add a per-Pal override only when a specific Pal needs stricter or looser limits than the global file.
7. Test with a small `PalTemplate.json` first before importing large templates.

## <span class='pd-badge pd-badge--beta'>Beta</span> common setups

### Allow most Pals, block a few

Use this when normal admin rewards are allowed, but certain Pals should not be imported.

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "BannedPalIDs": [
        "JetDragon",
        "BOSS_Anubis"
    ],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend"
    ],
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

### Only allow a curated list

Use this when player-imported templates should be limited to approved Pals.

```json
{
    "PalSelectionMode": "AllowOnlyListed",
    "AllowedPalIDs": [
        "Anubis",
        "Kirin",
        "WeaselDragon"
    ],
    "BannedPalIDs": [],
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 50,
    "MaxRank": 4,
    "PalSouls": {
        "Health": 10,
        "Attack": 10,
        "Defense": 10,
        "CraftSpeed": 10
    },
    "IVs": {
        "Health": 80,
        "AttackMelee": 80,
        "AttackShot": 80,
        "Defense": 80
    }
}
```

In this setup, only the three listed `PalID` values can be imported. Over-limit values are reduced to the configured maximums, and the listed passives are removed from the Pal.

## Default example

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "BannedPalIDs": [
        "JetDragon"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

## Per-Pal override example

### `Anubis.json`
```json
{
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 10,
    "MaxRank": 3,
    "PalSouls": {
        "Health": 5,
        "Attack": 5,
        "Defense": 5,
        "CraftSpeed": 5
    },
    "IVs": {
        "Health": 50,
        "AttackMelee": 50,
        "AttackShot": 50,
        "Defense": 50
    }
}
```
