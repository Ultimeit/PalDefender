# Installation

PalDefender ist von einer Windows-Umgebung abhängig. Wenn du deinen Palworld-Server auf einer Linux-basierten Maschine betreiben möchtest, musst du Wine oder Proton installieren.

Die Installation des Palworld-Servers selbst wird hier nicht behandelt. Wir empfehlen, einen Server bei Qonzer zu mieten und dabei diesen[Schritten](./Partnerships.md#how-to-get-the-10-discount) zu folgen。

---

## Windows

1. Lade <span class="file">PalDefender.zip</span> von <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a> herunter.
2. Entpacke den Inhalt von <span class="file">PalDefender.zip</span> und kopiere ihn in das PalServer-Unterverzeichnis: <span class="path">.../Pal/Binaries/Win64/</span>
3. Deine Ordnerstruktur sollte anschließend wie folgt aussehen:
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // Wird erzeugt (siehe Schritt 4)
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << Hier ablegen (siehe Schritt 2)
│   │       ├── d3d9.dll                          << Hier ablegen (siehe Schritt 2)
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
│           └── banlist.txt
├── PalServer.exe
├── steamclient.dll
└── <...>
```
4. Starte den Server einmal, damit die PalDefender-Ordnerstruktur unter <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> erzeugt wird. (siehe oben)
5. Passe anschließend die Konfiguration nach deinen Wünschen an. Empfehlung: Aktiviere die Whitelist.

---

## Linux (Wine / Proton)

**Wine oder Proton müssen installiert sein**, andernfalls funktionieren die folgenden Schritte nicht.

Die Einrichtung des Palworld-Servers unter Linux wird **nicht von PalDefender übernommen** und muss von dir selbst durchgeführt werden (inklusive Wine-/Proton-Konfiguration und Serverstart).

Sobald der Server unter Wine oder Proton **korrekt läuft**, kannst du die **Windows-Installationsanleitung unverändert übernehmen**, da sich die PalDefender-Installation dann nicht mehr unterscheidet.
