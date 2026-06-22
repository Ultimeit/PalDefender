# 📄 `PalSummon.json`

!!! note "<span class='pd-badge pd-badge--beta'>Beta</span>"
    Newly documented instructions on this page are marked with <span class='pd-badge pd-badge--beta'>Beta</span>. They are intended to make summon files easier to create and troubleshoot.

!!! tip "<span class='pd-badge pd-badge--beta'>Beta</span> related ID lookup"
    The summon file itself references a `PalTemplate`. If you need to edit that template, use [paldeck.cc/pals](https://paldeck.cc/pals) for `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) for passives, and [paldeck.cc/skills](https://paldeck.cc/skills) for skill IDs.

| Key               | Type   | Description                                                                             |
| ----------------- | ------ | --------------------------------------------------------------------------------------- |
| `PalTemplate`     | string | Required. File name of the `PalTemplate.json` to use (e.g., `"OPnubis.json"`). The file must exist in `Pals/Templates/`. |
| `Uncapturable`    | bool   | Optional. If `true`, the Pal cannot be captured by players. Defaults to `false` if omitted. |
| `X` / `Y` / `Z`   | float  | Required map coordinates where the Pal will be spawned. Use cmd `/getpos` to retrieve a player's current position. |
| `DisableStatuses` | array  | Optional list of status effects to disable for this Pal. Invalid or empty status names are skipped. Available statuses: `DrownCheck`, `Poison`, `Stun`, `Coma`, `Sleep`, `Overwork`, `Drown`, `FallDamage`, `LavaDamage`, `Burn`, `Wetness`, `Freeze`, `Electrical`, `Muddy`, `IvyCling`, `Darkness`, `CollectItem`. |

## <span class='pd-badge pd-badge--beta'>Beta</span> instruction set

1. Create the referenced Pal template first in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Create the summon file in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/`.
3. Name the summon file after the thing admins should type, for example `ArenaBoss.json` for `/summon ArenaBoss`.
4. Get coordinates in-game with `/getpos`. When using RCON, pass a player ID to `/getpos <UserId>`.
5. Keep `PalTemplate`, `X`, `Y`, and `Z` present. If any coordinate is missing, the summon should be treated as invalid.
6. Use `Uncapturable: true` for event bosses, raid bosses, or decorative Pals that players should not own.
7. Keep `DisableStatuses` short unless you have a reason to disable many states. Start with only the statuses that matter for the event.
8. Validate JSON before uploading. JSON does not allow comments or trailing commas.
9. Reload config or restart the server if your host does not pick up newly added files immediately.

## <span class='pd-badge pd-badge--beta'>Beta</span> setup walkthrough

1. Create a template first, for example `Pals/Templates/ArenaBoss.json`.
2. Test the template with `/givemepal_j ArenaBoss`. If the template fails there, fix the template before creating the summon file.
3. Stand where the Pal should appear and run `/getpos`. Copy the returned `X`, `Y`, and `Z` values.
4. Create `Pals/Summons/ArenaBossSpawn.json` and set `PalTemplate` to `ArenaBoss.json`.
5. Run `/summon ArenaBossSpawn`.
6. If the Pal appears too high, too low, or inside terrain, adjust `Z` first, then adjust `X` and `Y`.

## <span class='pd-badge pd-badge--beta'>Beta</span> example explanations

The minimal example below spawns `ArenaBoss.json` at a fixed coordinate, makes it uncapturable, and disables a short list of common crowd-control/status effects. This is useful for event bosses.

The full example shows the available `DisableStatuses` values. Do not copy every status by default; start with only the statuses that matter for your event.

## Minimal <span class='pd-badge pd-badge--beta'>Beta</span> example

```json
{
    "PalTemplate": "ArenaBoss.json",
    "Uncapturable": true,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": [
        "Poison",
        "Burn",
        "Freeze"
    ]
}
```

## Example

This file has to be stored at: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/ExamplePalSummon.json`
(`ExamplePalSummon` can be any unique name in that folder. This will be the command argument for `/summon`!)

```json
{
    "PalTemplate": "ExamplePalTemplate.json",
    "Uncapturable": true,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": [
        "DrownCheck",
        "Poison",
        "Stun",
        "Coma",
        "Sleep",
        "Overwork",
        "Drown",
        "FallDamage",
        "LavaDamage",
        "Burn",
        "Wetness",
        "Freeze",
        "Electrical",
        "Muddy",
        "IvyCling",
        "Darkness"
    ]
}
```
