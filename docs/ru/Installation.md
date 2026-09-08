# Установка

Для PalDefender требуется среда Windows. Чтобы разместить сервер Palworld на Linux, запустите сервер Windows и PalDefender через Wine или Proton.

Установка самого сервера Palworld здесь не рассматривается. Мы предлагаем приобрести сервер у Qonzer, следуя [инструкциям по получению скидки](./Partnerships.md).

---

## Windows

1. Загрузите <span class="file">PalDefender_Windows.zip</span> из <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub Releases</a>.
2. Извлеките содержимое <span class="file">PalDefender_Windows.zip</span> и поместите его в подкаталог PalServer:
<span class="path">.../Pal/Binaries/Win64/</span>
3. Ваша структура должна выглядеть так:
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
4. Запустите сервер один раз, чтобы сгенерировать файловую структуру PalDefender по адресу <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> (см. выше).
5. Просмотрите `Config.json` и отредактируйте его для своего сервера. Белый список игроков по умолчанию отключен; включите его, если вы собираетесь использовать сервер private/approved-player.

---

## Linux (Wine/Proton)

Wine или Proton **должны** быть установлены, иначе следующие шаги не будут работать.

Настройка сервера Palworld на Linux **не управляется PalDefender** и должна выполняться вами вручную (конфигурация Wine/Proton, запуск сервера и т. д.).

Как только сервер будет корректно работать под Wine или Proton, вы сможете **точно следовать инструкциям по установке Windows**, поскольку сама настройка PalDefender идентична.
