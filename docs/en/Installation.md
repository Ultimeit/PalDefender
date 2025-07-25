# Installation

PalDefender is dependend on a windows environment, if you plan to host your Palworld server on a Linux based machine, you will need to install Wine or Proton.

Installing a Palworld server itself is not covered here. We suggest getting a server from Qonzer following those [Steps](./Partnerships.md#how-to-get-the-10-discount).

---

## Windows

1. Donwload <span class="file">PalDefender_Windows.zip</span> from <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a>
2. Extract the contents of <span class="file">PalDefender_Windows.zip</span> and place it into your PalServer sub-directory: 
<span class="path">.../Pal/Binaries/Win64/</span>
3. Your structure should look like this:
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // Will be generated (Step 4)
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
│           └── banlist.txt
├── PalServer.exe
├── steamclient.dll
└── <...>
```
4. Start your server once to generate the PalDefender file structure at <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> (see above)
5. Edit the configuration to your favors. We recommend turning on the whitelist.

---

## Linux (Wine/Proton)

Proton or Wine has to be installed or the next steps will not work!

1. Install the Palworld build of <a href="https://github.com/Okaetsu/RE-UE4SS/releases/latest/" target="_blank">RE-UE4SS</a> on your server.
2. Donwload <span class="file">PalDefender_ProtonWine.zip</span> from <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a>
3. Extract the contents of <span class="file">PalDefender_ProtonWine.zip</span> and place it into your PalServer sub-directory: <span class="path">/Pal/Binaries/Win64/</span>
4. Your structure should look like this:
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── ue4ss/
│   │       │   ├── Mods/
│   │       │   │   ├── ActorDumperMod/           << Put here (Step 1)
│   │       │   │   ├── <...>/                       and other mods
│   │       │   │   ├── PalDefender/
│   │       │   │   │   ├── dlls/
│   │       │   │   │   │   └── main.dll          << Put here (Step 3)
│   │       │   │   │   └── enabled.txt           << Put here (Step 3)
│   │       │   │   ├── mods.txt                  << Put here (Step 1)
│   │       │   │   └── mods.json                 << Put here (Step 1)
│   │       │   ├── MemberVariableLayout.ini      << Put here (Step 1)
│   │       │   ├── UE4SS.dll                     << Put here (Step 1)
│   │       │   └── UE4SS-settings.ini            << Put here (Step 1)
│   │       ├── PalDefender/                      // Will be generated (Step 5)
│   │       ├── <...>
│   │       ├── dwmapi.dll                        << Put here (Step 1)
│   │       ├── PalDefender.dll                   << Put here (Step 3)
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
5. Start your server once to generate the PalDefender file structure at <span class="path">/Pal/Binaries/Win64/PalDefender/</span> (see above)
6. Edit the configuration to your favors. We recommend turning on the whitelist.