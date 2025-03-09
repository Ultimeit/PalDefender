![PalDefender Logo](/.github/images/LOGO.jpg)
*LOGO made by [Jia](<https://www.fiverr.com/javeriahjaved/design-a-unique-sports-mascot-esports-and-gaming-logo>)* !

# PalDefender (PalWorld Server AntiCheat)
**Version:** 1.1291

#### English / [简体中文](/README_ZH_CN.md)

## **Get the best servers for modding at [Qonzer](https://qonzer.com/aff.php?aff=61) *(Affiliate Link)*.** 
*They support PalDefender right out of the box—no special setup or technical knowledge needed. It just works.*

**A 10% Discount code for qonzer servers can be found on our Discord! Check out the server-host channel.**

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/T6T014OZZB)

[![Discord Server](https://img.shields.io/badge/-Join%20our%20Discord-111111?style=for-the-badge&logo=discord)](https://discord.com/invite/bdTxPbwSEW)
[![Static Badge](https://img.shields.io/badge/-Nexus%20Mods-111111?style=for-the-badge&logo=nexusmods)](https://www.nexusmods.com/palworld/mods/451)

<br>

## Table of Contents
* [About](#about-)
* [Requirements](#requirements-)
* [Installation](#installation-)
   - [Windows](#windows)
   - [Linux (Wine/Proton)](#linux-wineproton)
* [Features](#features-)
* [Wiki](Wiki/README.md)
* [Authors](#authors-)
* [Credits](#credits-)
* [Afterwords](#afterwords-)

## About [↑](#paldefender-palworld-server-anticheat)

Implements comprehensive server-side validation to prevent a wide range of known and some yet undiscovered cheats, exploits, and crashes. Before executing any player action, PalDefender checks for potential cheating behavior. Depending on the server's configuration, players attempting such actions are warned, kicked, banned, or IP banned. Currently, this feature is in beta and is available exclusively for Windows-based dedicated servers. **Any experienced Linux dev is welcome to help us out.**

The code is closed source and we dont have any plans to release it.

<br>

## Requirements [↑](#paldefender-palworld-server-anticheat)
- [Microsoft Visual C++ Latest Redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  I'm not exactly sure how this works for Proton or Wine but related of the feedback it seemed to work out of the box.

<br>

## Installation [↑](#paldefender-palworld-server-anticheat)

### Windows
1. Download the latest release at [NexusMods.com](https://www.nexusmods.com/palworld/mods/451)
2. Extract the contents and place it into your PalServer sub-directory `Pal\Binaries\Win64`
   It should look like this:
   ```
   Palworld_Server/
   ├── Engine/
   ├── Pal/
   │   ├── Binaries/
   │   │   └── Win64
   │   │       ├── config/
   │   │       ├── PalDefender/                      # Will be generated
   │   │       ├── <...>
   │   │       ├── PalDefender.dll                   # << Put here
   │   │       ├── version.dll                       # << Put here (Windows only)
   │   │       ├── PalServer-Win64-Shipping-Cmd.exe
   │   │       └── PalServer-Win64-Shipping.exe
   │   ├── Content/
   │   ├── Plugins/
   │   └── Saved/
   ├── PalServer.exe
   ├── steamclient.dll
   └── <...>
   ```
3. Start your server once to generate the config file `Config.json`, which will be generated at `./PalDefender/Config.json`.

### Linux (Wine/Proton)
1. Install a Palworld Proton/Wine server (This won't be covered here).
2. Install [UE4SS](https://github.com/UE4SS-RE/RE-UE4SS) on your server.
3. Follow the Windows instructions.

## Features [↑](#paldefender-palworld-server-anticheat)

* Cheat & Exploit detection, prevention and punishment
* More Admin commands (including RCON)
* IP banning System
* IP whitelist for Admin commands (so cheaters can't use them)
* Chat logging
* Unreal Engine Network logging
* Configurable cheating punishments
* PvP damage limiting (although we would suggest not enabling PvP at all)
* A few game mechanic tweaks such as Pal Enhancement limitations or disable Butchering

<br>

## Wiki [↑](#paldefender-palworld-server-anticheat)

All around PalDefender and its usage can be found in the [Wiki](Wiki/README.md).

<br>

## Authors [↑](#paldefender-palworld-server-anticheat)

- [Ultimeit](https://github.com/Ultimeit)
- [Zvendson](https://github.com/Zvendson)

<br>

## Credits [↑](#paldefender-palworld-server-anticheat)

* [Pocketpair, Inc.](https://www.pocketpair.jp/palworld)
* [Unreal Engine](https://www.unrealengine.com) - Epic Games

<br>

## Afterwords [↑](#paldefender-palworld-server-anticheat)

**私たちは、[Pocketpair, Inc.](https://www.pocketpair.jp/palworld)による素晴らしい仕事に感謝の意を表したいと思います。色鮮やかな世界や、パルとのダイナミックなインタラクション、そして創造的なデザインは、チームの献身と情熱を見事に表しています。コミュニティの一員として、私たちはPalServer向けのプラグインを開発し、セキュリティを強化し、潜在的な悪用から守ることでPalworldをサポートしています**

**私たちは今後も、Palworldサーバーに最高水準のセキュリティと保護を提供できるよう努め続けます。皆様からのフィードバックは非常に貴重で、心から感謝しています。**<br>
~ [Zvend](https://github.com/Zvendson)

> *We want to express our gratitude to [Pocketpair, Inc.](https://www.pocketpair.jp/palworld) for their incredible work on Palworld. The vibrant world, dynamic interactions with Pals, and creative design showcase the team's dedication and passion. As a community, we are also working to support Palworld by developing a plugin for the PalServer that enhances security and protects it from potential exploits.*
<br><br>
*We will continue striving to provide the highest level of security and protection for your Palworld server. Your feedback is invaluable, and we truly appreciate it.*
