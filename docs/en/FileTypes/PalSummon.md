# 📄 `PalSummon.json`

| Key               | Type   | Description                                                                             |
| ----------------- | ------ | --------------------------------------------------------------------------------------- |
| `PalTemplate`     | string | File name of the `PalTemplate.json` to use (e.g., `"OPnubis.json"`).                    |
| `Uncapturable`    | bool   | If `true`, the Pal cannot be captured by players.                                       |
| `X` / `Y` / `Z`   | float  | Map coordinates where the Pal will be spawned. Use cmd `/getpos` to retrieve your current position. |
| `DisableStatuses` | array  | List of status effects to disable for this Pal. Available statuses: `DrownCheck`, `Poison`, `Stan`, `Coma`, `Sleep`, `Overwork`, `Drown`, `FallDamage`, `LavaDamage`, `Burn`, `Wetness`, `Freeze`, `Electrical`, `Muddy`, `IvyCling`, `Darkness`, `CollectItem`. |
