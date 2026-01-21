# 📄 `PalSummon.json`

| Key               | Type   | Description                                                                             |
| ----------------- | ------ | --------------------------------------------------------------------------------------- |
| `PalTemplate`     | string | File name of the `PalTemplate.json` to use (e.g., `"OPnubis.json"`).                    |
| `Uncapturable`    | bool   | If `true`, the Pal cannot be captured by players.                                       |
| `X` / `Y` / `Z`   | float  | Map coordinates where the Pal will be spawned. Use cmd `/getpos` to retrieve your current position. |
| `DisableStatuses` | array  | List of status effects to disable for this Pal. Available statuses: `DrownCheck`, `Poison`, `Stun`, `Coma`, `Sleep`, `Overwork`, `Drown`, `FallDamage`, `LavaDamage`, `Burn`, `Wetness`, `Freeze`, `Electrical`, `Muddy`, `IvyCling`, `Darkness`, `CollectItem`. |

## Example:

This file has to be stored at: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/ExamplePalSummon.json`
(`ExamplePalSummon` can be any unique name in that folder. This will be the command argument for `/summon`!)

```json
{
    "PalTemplate": "ExamplePalTemplate.json",  // This is the reference filename in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`
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