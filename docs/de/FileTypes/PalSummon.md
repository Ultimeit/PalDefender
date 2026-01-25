# 📄 `PalSummon.json`

| Key               | Typ    | Beschreibung                                                                 |
| ----------------- | ------ | ---------------------------------------------------------------------------- |
| `PalTemplate`     | string | Dateiname der zu verwendenden `PalTemplate.json` (z. B. `"OPnubis.json"`). |
| `Uncapturable`    | bool   | Wenn `true`, kann der Pal nicht von Spielern gefangen werden.               |
| `X` / `Y` / `Z`   | float  | Kartenkoordinaten, an denen der Pal gespawnt wird. Verwende den Befehl `/getpos`, um deine aktuelle Position zu ermitteln. |
| `DisableStatuses` | array  | Liste der zu deaktivierenden Statuseffekte für diesen Pal. Verfügbare Status: `DrownCheck`, `Poison`, `Stun`, `Coma`, `Sleep`, `Overwork`, `Drown`, `FallDamage`, `LavaDamage`, `Burn`, `Wetness`, `Freeze`, `Electrical`, `Muddy`, `IvyCling`, `Darkness`, `CollectItem`. |

## Beispiel:

Diese Datei muss unter folgendem Pfad gespeichert werden:
`<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/ExamplePalSummon.json`
(`ExamplePalSummon` kann ein beliebiger eindeutiger Name in diesem Ordner sein. Dieser Name wird als Befehlsargument für `/summon` verwendet!)

```json
{
    "PalTemplate": "ExamplePalTemplate.json",  // Dies ist der Referenzdateiname unter `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`
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
