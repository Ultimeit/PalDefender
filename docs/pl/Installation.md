# Instalacja

PalDefender wymaga środowiska Windows. Aby uruchomić serwer Palworld w systemie Linux, użyj windowsowej wersji serwera i PalDefender przez Wine lub Proton.

Ta strona nie opisuje instalacji samego serwera Palworld. Polecamy serwer w Qonzer — skorzystaj z [instrukcji uzyskania rabatu](./Partnerships.md#permanent-discount).

---

## Windows

1. Pobierz <span class="file">PalDefender_Windows.zip</span> ze strony <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">wydań na GitHubie</a>.
2. Rozpakuj <span class="file">PalDefender_Windows.zip</span> i umieść jego zawartość w podkatalogu PalServer:
<span class="path">.../Pal/Binaries/Win64/</span>
3. Struktura katalogów powinna wyglądać następująco:
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // Zostanie utworzony (krok 4)
│   │       │   ├── Banlist.json
│   │       │   ├── Config.json
│   │       │   ├── Pals/
│   │       │   └── RESTAPI/
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << Umieść tutaj (krok 2)
│   │       ├── version.dll                       << Umieść tutaj (krok 2)
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
4. Uruchom serwer raz, aby utworzyć strukturę plików PalDefender w <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> (patrz wyżej).
5. Sprawdź `Config.json` i dostosuj go do swojego serwera. Lista dozwolonych graczy jest domyślnie wyłączona. Włącz ją, jeśli serwer ma być prywatny lub dostępny tylko dla zatwierdzonych graczy.

---

## Linux (Wine/Proton)

Wine lub Proton **musi** być zainstalowany. Bez niego poniższe kroki nie zadziałają.

PalDefender **nie zarządza konfiguracją serwera Palworld w systemie Linux**. Konfigurację Wine/Proton, uruchamianie serwera i pozostałe czynności musisz wykonać samodzielnie.

Gdy serwer działa poprawnie przez Wine lub Proton, **wykonaj te same kroki instalacji co w systemie Windows**. Instalacja samego PalDefender przebiega identycznie.
