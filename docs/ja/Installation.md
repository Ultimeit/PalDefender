# インストール

PalDefender には Windows 環境が必要です。 Linux で Palworld サーバーをホストするには、Wine または Proton を介して Windows サーバーと PalDefender を実行します。

Palworld サーバー自体のインストールについては、ここでは説明しません。[割引手順](./Partnerships.md)に従って、Qonzer からサーバーを入手することをお勧めします。

---

## Windows

1. <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub リリース</a> から <span class="file">PalDefender_Windows.zip</span> をダウンロードします。
2. <span class="file">PalDefender_Windows.zip</span> の内容を抽出し、PalServer サブディレクトリに配置します。
<span class="path">.../Pal/Binaries/Win64/</span>
3. 構造は次のようになります。
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
4. サーバーを一度起動して、<span class="path">.../Pal/Binaries/Win64/PalDefender/</span> に PalDefender ファイル構造を生成します (上記を参照)。
5. `Config.json` を確認し、サーバーに合わせて編集します。プレーヤーのホワイトリストはデフォルトでは無効になっています。プライベート/承認済みプレーヤーサーバーを操作する場合は、これを有効にしてください。

---

## Linux (ワイン/プロトン)

Wine または Proton **がインストールされている必要があります**。インストールされていないと、次の手順が機能しません。

Linux 上の Palworld サーバー セットアップは **PalDefender** によって管理されず、手動で処理する必要があります (Wine/Proton の構成、サーバーの起動など)。

Wine または Proton でサーバーが正しく実行されたら、PalDefender セットアップ自体は同一であるため、**Windows のインストール手順に正確に従うことができます**。
