# 安装

PalDefender 依赖 Windows 环境。如果你计划在 Linux 系统上托管 Palworld 服务器，需要安装 Wine 或 Proton。

这里不介绍 Palworld 服务器本身的安装。我们建议使用 Qonzer 服务器，并按照这些[步骤](./Partnerships.md)操作。

---

## Windows

1. 从 <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub/releases</a> 下载 <span class="file">PalDefender_Windows.zip</span>。
2. 解压 <span class="file">PalDefender_Windows.zip</span>，并将内容放入 PalServer 子目录：
<span class="path">.../Pal/Binaries/Win64/</span>
3. 目录结构应如下所示：
```yaml
Palworld_Server/
├── Engine/
├── Pal/
│   ├── Binaries/
│   │   └── Win64
│   │       ├── config/
│   │       ├── PalDefender/                      // 将会生成（步骤 4）
│   │       │   ├── Banlist.json
│   │       │   ├── Config.json
│   │       │   ├── Pals/
│   │       │   └── RESTAPI/
│   │       ├── <...>
│   │       ├── PalDefender.dll                   << 放在这里（步骤 2）
│   │       ├── d3d9.dll                          << 放在这里（步骤 2）
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
4. 启动服务器一次，让 PalDefender 在 <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> 生成文件结构（见上方）。
5. 按你的需求编辑配置。我们建议启用白名单。

---

## Linux (Wine/Proton)

必须安装 Wine 或 Proton，否则以下步骤无法工作。

Linux 上的 Palworld 服务器设置**不由 PalDefender 管理**，需要你手动处理（Wine/Proton 配置、服务器启动等）。

当服务器能在 Wine 或 Proton 下正常运行后，你可以**完全按照 Windows 安装说明操作**，因为 PalDefender 本身的设置流程相同。
