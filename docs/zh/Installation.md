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
│   │       ├── d3d9.dll                          << 放置于此（步骤 2）
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

必须先安装 **Wine 或 Proton**，否则以下步骤将无法工作。

Palworld 服务器在 Linux 下的部署 **不由 PalDefender 管理**，需要你自行完成（包括 Wine / Proton 的配置、服务器启动等）。

当服务器能够在 Wine 或 Proton 环境下 **正常运行** 后，**PalDefender 的安装步骤与 Windows 完全一致**，可以直接按照 Windows 的安装说明进行。
