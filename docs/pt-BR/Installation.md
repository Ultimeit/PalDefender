# Instalação

PalDefender requer um ambiente Windows. Para hospedar um servidor Palworld em Linux, execute o servidor Windows e PalDefender através do Wine ou Proton.

A instalação de um servidor Palworld em si não é abordada aqui. Sugerimos adquirir um servidor da Qonzer seguindo as [instruções de desconto](./Partnerships.md).

---

## Windows

1. Baixe <span class="file">PalDefender_Windows.zip</span> de <a href="https://github.com/Ultimeit/PalDefender/releases/latest/" target="_blank">GitHub versões</a>.
2. Extraia o conteúdo de <span class="file">PalDefender_Windows.zip</span> e coloque-o em seu subdiretório PalServer:
<span class="path">.../Pal/Binaries/Win64/</span>
3. Sua estrutura deve ficar assim:
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
4. Inicie seu servidor uma vez para gerar a estrutura do arquivo PalDefender em <span class="path">.../Pal/Binaries/Win64/PalDefender/</span> (veja acima)
5. Revise `Config.json` e edite-o para seu servidor. A lista de permissões do jogador está desabilitada por padrão; habilite-o se pretende operar um servidor private/approved-player.

---

## Linux (Wine/Proton)

Wine ou Proton **devem** estar instalados, caso contrário as etapas a seguir não funcionarão.

A configuração do servidor Palworld em Linux **não é gerenciada por PalDefender** e deve ser tratada manualmente por você (configuração de Wine/Proton, inicialização do servidor, etc.).

Assim que o servidor estiver funcionando corretamente no Wine ou Proton, você pode **seguir exatamente as instruções de instalação do Windows**, pois a configuração do PalDefender em si é idêntica.
