# :octicons-file-16: `PalSummon.json`

!!! tip "Zugehörige ID-Suche"
    Die Summon-Datei verweist selbst auf ein `PalTemplate`. Wenn du dieses Template bearbeiten musst, nutze [paldeck.cc/pals](https://paldeck.cc/pals) für `PalID`, [paldeck.cc/passives](https://paldeck.cc/passives) für Passives und [paldeck.cc/skills](https://paldeck.cc/skills) für Skill-IDs.

| Schlüssel               | Typ   | Beschreibung                                                                             |
| ----------------- | ------ | --------------------------------------------------------------------------------------- |
| `PalTemplate`     | string | Erforderlich. Dateiname der zu verwendenden `PalTemplate.json` (z. B. `"OPnubis.json"`). Die Datei muss in `Pals/Templates/` existieren. |
| `Uncapturable`    | bool   | Optional. Wenn `true`, kann der Pal nicht von Spielern gefangen werden. Ohne Angabe gilt `false`. |
| `X` / `Y` / `Z`   | float  | Erforderliche Kartenkoordinaten, an denen der Pal gespawnt wird. Nutze `/getpos`, um die aktuelle Position eines Spielers abzurufen. |
| `DisableStatuses` | array  | Optionale Liste von Statuseffekten, die für diesen Pal deaktiviert werden. Ungültige oder leere Statusnamen werden übersprungen. Verfügbare Status: `DrownCheck`, `Poison`, `Stun`, `Coma`, `Sleep`, `Overwork`, `Drown`, `FallDamage`, `LavaDamage`, `Burn`, `Wetness`, `Freeze`, `Electrical`, `Muddy`, `IvyCling`, `Darkness`, `CollectItem`. |

## Anleitung

1. Erstelle zuerst das referenzierte Pal-Template in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Erstelle die Summon-Datei in `<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/`.
3. Benenne die Summon-Datei nach dem Argument, das Admins eingeben sollen, zum Beispiel `ArenaBoss.json` für `/summon ArenaBoss`.
4. Ermittle Koordinaten im Spiel mit `/getpos`. Bei RCON gib eine Spieler-ID an: `/getpos <UserId>`.
5. `PalTemplate`, `X`, `Y` und `Z` müssen vorhanden sein. Fehlt eine Koordinate, sollte die Summon-Datei als ungültig gelten.
6. Nutze `Uncapturable: true` für Eventbosse, Raidbosse oder dekorative Pals, die Spieler nicht besitzen sollen.
7. Halte `DisableStatuses` kurz, außer du hast einen Grund, viele Zustände zu deaktivieren. Beginne nur mit den Statuswerten, die für das Event wichtig sind.
8. Validiere JSON vor dem Hochladen. JSON erlaubt keine Kommentare oder nachgestellten Kommas.
9. Lade die Konfiguration neu oder starte den Server neu, falls dein Host neu hinzugefügte Dateien nicht sofort übernimmt.

## Einrichtungsschritte

1. Erstelle zuerst ein Template, zum Beispiel `Pals/Templates/ArenaBoss.json`.
2. Teste das Template mit `/givemepal_j ArenaBoss`. Wenn es dort fehlschlaegt, repariere zuerst das Template, bevor du die Summon-Datei erstellst.
3. Stelle dich an die Stelle, an der der Pal erscheinen soll, und führe `/getpos` aus. Kopiere die zurückgegebenen Werte `X`, `Y` und `Z`.
4. Erstelle `Pals/Summons/ArenaBossSpawn.json` und setze `PalTemplate` auf `ArenaBoss.json`.
5. Führe `/summon ArenaBossSpawn` aus.
6. Wenn der Pal zu hoch, zu niedrig oder im Gelände erscheint, passe zuerst `Z` an und danach `X` und `Y`.

## Erklärung der Beispiele

Das Minimalbeispiel unten spawnt `ArenaBoss.json` an festen Koordinaten, macht ihn unfangbar und deaktiviert eine kurze Liste üblicher Kontroll-/Statuseffekte. Das ist für Eventbosse nützlich.

Das vollständige Beispiel zeigt die verfügbaren `DisableStatuses`-Werte. Kopiere nicht standardmäßig jeden Status; beginne nur mit den Werten, die für dein Event wichtig sind.

## Minimalbeispiel

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

## Beispiel

Diese Datei muss hier gespeichert werden: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Summons/ExamplePalSummon.json`
(`ExamplePalSummon` kann ein beliebiger eindeutiger Name in diesem Ordner sein. Das ist später das Befehlsargument für `/summon`!)

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
