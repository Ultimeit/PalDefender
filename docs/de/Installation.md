# Installation

PalDefender benoetigt eine Windows-Umgebung. Wenn du deinen Palworld-Server auf einem Linux-basierten System hosten willst, musst du Wine oder Proton installieren.

Die Installation des Palworld-Servers selbst wird hier nicht behandelt. Wir empfehlen einen Server von Qonzer; folge dafür diesen [Schritten](./Partnerships.md).

---

## Windows

1. Lade <span class="file">PalDefender_Windows.zip</span> von <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a> herunter.
2. Entpacke den Inhalt von <span class="file">PalDefender_Windows.zip</span> und lege ihn in dein PalServer-Unterverzeichnis:
<span class="path">.../Pal/Binaries/Win64/</span>
3. Deine Struktur sollte so aussehen:
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // Wird generiert (Schritt 4)
│   │       │   ├── Banlist.json
│   │       │   ├── Config.json
│   │       │   ├── Pals/
│   │       │   └── RESTAPI/
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << Hier ablegen (Schritt 2)
│   │       ├── d3d9.dll                          << Hier ablegen (Schritt 2)
│   │       ├── PalServer-Win64-Shipping-Cmd.exe
│   │       └── PalServer-Win64-Shipping.exe
│   ├── Content/
│   ├── Plugins/
│   └── Saved/
│       ├── Config/
│       │   ├── CrashReportClient/
│       │   └── WindowsServer/
│       │       ├── GameUserSettings.ini
│       │       ├── <...>
│       │       └── PalWorldSettings.ini
│       ├── Crashes/
│       ├── <...>
│       └── SaveGames/
│           ├── 0/<WorldGUID>/
│           │     ├── backup/
│           │     ├── Players/
│           │     ├── Level.sav
│           │     └── LevelMeta.sav
├── PalServer.exe
├── steamclient.dll
└── <...>
```
4. Starte deinen Server einmal, damit PalDefender die Dateistruktur unter <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> erzeugt (siehe oben).
5. Passe die Konfiguration nach deinen Wuenschen an. Wir empfehlen, die Whitelist zu aktivieren.

---

## Linux (Wine/Proton)

Wine oder Proton **muss** installiert sein, sonst funktionieren die folgenden Schritte nicht.

Die Palworld-Servereinrichtung unter Linux wird **nicht von PalDefender verwaltet** und muss von dir manuell vorgenommen werden (Wine-/Proton-Konfiguration, Serverstart usw.).

Sobald der Server korrekt unter Wine oder Proton läuft, kannst du **exakt der Windows-Installationsanleitung folgen**, da die PalDefender-Einrichtung identisch ist.
