# 安装

PalDefender 依赖于 Windows 环境，如果您计划在基于 Linux 的机器上托管 Palworld 服务器，您需要安装 Wine 或 Proton。

本文不涵盖 Palworld 服务器本身的安装。我们建议按照这些[步骤](./Partnerships.md#how-to-get-the-10-discount)从 Qonzer 获取服务器。

---

## Windows

1. 从 <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a> 下载 <span class="file">PalDefender_Windows.zip</span>
2. 解压 <span class="file">PalDefender_Windows.zip</span> 的内容并将其放置到您的 PalServer 子目录中： 
<span class="path">.../Pal/Binaries/Win64/</span>
3. 您的目录结构应该如下所示：
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // 将生成（步骤 4）
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << 放置于此（步骤 2）
│   │       ├── version.dll                       << 放置于此（步骤 2）
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
4. 启动服务器一次以在 <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> 生成 PalDefender 文件结构（见上文）
5. 根据您的喜好编辑配置。我们建议开启白名单。

---

## Linux (Wine/Proton)

必须先安装 Proton 或 Wine，否则后续步骤将无法工作！

1. 在您的服务器上安装 <a href="https://github.com/Okaetsu/RE-UE4SS/releases/latest/" target="_blank">RE-UE4SS</a> 的 Palworld 版本。
2. 从 <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a> 下载 <span class="file">PalDefender_ProtonWine.zip</span>
3. 解压 <span class="file">PalDefender_ProtonWine.zip</span> 的内容并将其放置到您的 PalServer 子目录中：<span class="path">/Pal/Binaries/Win64/</span>
4. 您的目录结构应该如下所示：
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── ue4ss/
│   │       │   ├── Mods/
│   │       │   │   ├── ActorDumperMod/           << 放置于此（步骤 1）
│   │       │   │   ├── <...>/                       以及其他模组
│   │       │   │   ├── PalDefender/
│   │       │   │   │   ├── dlls/
│   │       │   │   │   │   └── main.dll          << 放置于此（步骤 3）
│   │       │   │   │   └── enabled.txt           << 放置于此（步骤 3）
│   │       │   │   ├── mods.txt                  << 放置于此（步骤 1）
│   │       │   │   └── mods.json                 << 放置于此（步骤 1）
│   │       │   ├── MemberVariableLayout.ini      << 放置于此（步骤 1）
│   │       │   ├── UE4SS.dll                     << 放置于此（步骤 1）
│   │       │   └── UE4SS-settings.ini            << 放置于此（步骤 1）
│   │       ├── PalDefender/                      // 将生成（步骤 5）
│   │       ├── <...>
│   │       ├── dwmapi.dll                        << 放置于此（步骤 1）
│   │       ├── PalDefender.dll                   << 放置于此（步骤 3）
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
5. 启动服务器一次以在 <span class="path">/Pal/Binaries/Win64/PalDefender/</span> 生成 PalDefender 文件结构（见上文）
6. 根据您的喜好编辑配置。我们建议开启白名单。