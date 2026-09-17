# 설치

PalDefender는 Windows 환경이 필요합니다. Linux에서 Palworld 서버를 운영하려면 Wine 또는 Proton을 통해 Windows용 서버와 PalDefender를 실행하세요.

Palworld 서버 자체의 설치 방법은 여기서 다루지 않습니다. [할인 적용 안내](./Partnerships.md#permanent-discount)를 따라 Qonzer 서버를 이용하는 것을 권장합니다.

---

## Windows

1. <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub 릴리스</a>에서 <span class="file">PalDefender_Windows.zip</span>을 다운로드하세요.
2. <span class="file">PalDefender_Windows.zip</span>의 압축을 풀고 내용을 다음 PalServer 하위 디렉터리에 넣으세요.
<span class="path">.../Pal/Binaries/Win64/</span>
3. 디렉터리 구조는 다음과 같아야 합니다.
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // 4단계에서 생성됨
│   │       │   ├── Banlist.json
│   │       │   ├── Config.json
│   │       │   ├── Pals/
│   │       │   └── RESTAPI/
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << 여기에 넣기 (2단계)
│   │       ├── version.dll                       << 여기에 넣기 (2단계)
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
4. 서버를 한 번 실행하여 <span class="path">.../Pal/Binaries/Win64/PalDefender/</span>에 위에서 안내한 PalDefender 파일 구조를 생성하세요.
5. `Config.json`을 확인하고 서버에 맞게 수정하세요. 플레이어 허용 목록은 기본적으로 꺼져 있습니다. 비공개 서버나 승인된 플레이어만 접속할 수 있는 서버를 운영하려면 켜세요.

---

## Linux (Wine/Proton)

Wine 또는 Proton이 **반드시** 설치되어 있어야 합니다. 설치되어 있지 않으면 다음 절차를 진행할 수 없습니다.

Linux의 Palworld 서버 설정은 **PalDefender가 관리하지 않습니다**. Wine/Proton 설정, 서버 실행 등의 작업은 직접 진행해야 합니다.

Wine 또는 Proton에서 서버가 정상적으로 실행되면 **Windows 설치 절차를 그대로 따르면 됩니다**. PalDefender 자체의 설치 방법은 동일합니다.
