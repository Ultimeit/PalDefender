# Mise en place

PalDefender nécessite un environnement Windows. Pour héberger un serveur Palworld sur Linux, exécutez le serveur Windows et PalDefender via Wine ou Proton.

L'installation d'un serveur Palworld lui-même n'est pas abordée ici. Nous vous suggérons d'obtenir un serveur auprès de Qonzer en suivant les [instructions de remise](./Partnerships.md).

---

## Windows

1. Téléchargez <span class="file">PalDefender_Windows.zip</span> à partir des versions <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub</a>.
2. Extrayez le contenu de <span class="file">PalDefender_Windows.zip</span> et placez-le dans votre sous-répertoire PalServer :
<span class="path">.../Pal/Binaries/Win64/</span>
3. Votre structure devrait ressembler à ceci :
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // Will be generated (Step 4)
│   │       │   ├── Banlist.json
│   │       │   ├── Config.json
│   │       │   ├── Pals/
│   │       │   └── RESTAPI/
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << Put here (Step 2)
│   │       ├── version.dll                       << Put here (Step 2)
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
4. Démarrez votre serveur une fois pour générer la structure de fichiers PalDefender à <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> (voir ci-dessus)
5. Vérifiez `Config.json` et modifiez-le pour votre serveur. La liste blanche des joueurs est désactivée par défaut ; activez-le si vous avez l’intention d’exploiter un serveur private/approved-player.

---

## Linux (Wine/Proton)

Wine ou Proton **doivent** être installés, sinon les étapes suivantes ne fonctionneront pas.

La configuration du serveur Palworld sur Linux n'est **pas gérée par PalDefender** et doit être gérée manuellement par vous (configuration Wine/Proton, démarrage du serveur, etc.).

Une fois que le serveur fonctionne correctement sous Wine ou Proton, vous pouvez **suivre exactement les instructions d'installation de Windows**, car la configuration de PalDefender elle-même est identique.
