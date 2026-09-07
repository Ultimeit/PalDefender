# Installation

PalDefender requires a Windows environment. To host a Palworld server on Linux, run the Windows server and PalDefender through Wine or Proton.

Installing a Palworld server itself is not covered here. We suggest getting a server from Qonzer by following the [discount instructions](./Partnerships.md#how-to-get-the-permanent-15-discount).

---

## Windows

1. Download <span class="file">PalDefender_Windows.zip</span> from <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub Releases</a>.
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
4. Start your server once to generate the PalDefender file structure at <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> (see above)
5. Review `Config.json` and edit it for your server. The player whitelist is disabled by default; enable it if you intend to operate a private/approved-player server.

---

## Linux (Wine/Proton)

Wine or Proton **must** be installed, otherwise the following steps will not work.

The Palworld server setup on Linux is **not managed by PalDefender** and must be handled manually by you (Wine/Proton configuration, server startup, etc.).

Once the server is running correctly under Wine or Proton, you can **follow the Windows installation instructions exactly**, as the PalDefender setup itself is identical.
