![PalDefender Logo](/.github/images/LOGO.jpg)
*LOGO made by [Jia](<https://www.fiverr.com/javeriahjaved/design-a-unique-sports-mascot-esports-and-gaming-logo>)* !

# PalDefender (幻兽帕鲁服务器反作弊)
**Version:** 1.1291

### [English](/README.md) / 简体中文

## **Get the best servers for modding at [Qonzer](https://qonzer.com/aff.php?aff=61) *(Affiliate Link)*.** 
*They support PalDefender right out of the box—no special setup or technical knowledge needed. It just works.*

**A 10% Discount code for qonzer servers can be found on our Discord! Check out the server-host channel.**

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/T6T014OZZB)

[![Discord Server](https://img.shields.io/badge/-Join%20our%20Discord-111111?style=for-the-badge&logo=discord)](https://discord.com/invite/bdTxPbwSEW)
[![Static Badge](https://img.shields.io/badge/-Nexus%20Mods-111111?style=for-the-badge&logo=nexusmods)](https://www.nexusmods.com/palworld/mods/451)

<br>

## 目录
* [关于](#关于-)
* [需求](#需求-)
* [安装](#安装-)
   - [Windows](#windows)
   - [Linux (Wine/Proton)](#linux-wineproton)
* [功能](#功能-)
* [Wiki](Wiki/README_ZH_CN.md)
* [作者](#作者-)
* [致谢](#致谢-)
* [后记](#后记-)

## 关于 [↑](#paldefender-幻兽帕鲁服务器反作弊)

实现了全面的服务端验证，防止已知和一些尚未发现的作弊、漏洞和崩溃。PalDefender 在执行任何玩家操作之前会检查潜在的作弊行为。根据服务器的配置，尝试这些操作的玩家会被警告、踢出、封禁或 IP 封禁。目前，这一功能处于测试阶段，仅在基于 Windows 的服务器上可用。**任何有经验的 Linux 开发者都欢迎来帮助我们。**

代码是闭源的，我们没有计划发布它。

<br>

## 需求 [↑](#paldefender-幻兽帕鲁服务器反作弊)

- [Microsoft Visual C++ 最新版本的可再发行组件](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)
  我不确定在 Proton 或 Wine 上如何使用，但根据反馈，它似乎可以开箱即用。

<br>

## 安装 [↑](#paldefender-幻兽帕鲁服务器反作弊)

### Windows

1. 在 [NexusMods.com](https://www.nexusmods.com/palworld/mods/451) 下载最新版本
2. 解压内容并将其放入你的 PalServer 子目录 `Pal\Binaries\Win64`
   目录结构应如下所示：
   ```
   Palworld_Server/
   ├── Engine/
   ├── Pal/
   │   ├── Binaries/
   │   │   └── Win64
   │   │       ├── config/
   │   │       ├── PalDefender/                      # 将生成此文件夹
   │   │       ├── <...>
   │   │       ├── PalDefender.dll                   # << 放在此处
   │   │       ├── version.dll                       # << 放在此处 (Windows only)
   │   │       ├── PalServer-Win64-Shipping-Cmd.exe
   │   │       └── PalServer-Win64-Shipping.exe
   │   ├── Content/
   │   ├── Plugins/
   │   └── Saved/
   ├── PalServer.exe
   ├── steamclient.dll
   └── <...>
   ```
3. 请先启动您的服务器一次，以生成配置文件 `Config.json`，该文件将生成在 `./PalDefender/Config.json`。

### Linux (Wine/Proton)

1. 安装 Palworld Proton/Wine 服务器（此部分不在本文涵盖范围内）。
2. 在服务器上安装 [UE4SS](https://github.com/UE4SS-RE/RE-UE4SS)。
3. 按照 Windows 安装步骤操作。

## 功能 [↑](#paldefender-幻兽帕鲁服务器反作弊)

* 作弊和漏洞检测、预防与惩罚
* 更多的管理员命令（包括 RCON）
* IP 封禁系统
* 管理员命令的 IP 白名单（防止作弊者使用管理员命令）
* 聊天记录
* RCON REST网络日志
* 可配置的作弊惩罚
* PvP 伤害限制（尽管我们建议完全禁用 PvP）
* 一些游戏机制调整，如限制帕鲁强化或禁用肢解

<br>

## Wiki [↑](#paldefender-幻兽帕鲁服务器反作弊)

关于 PalDefender 和它的使用，详细信息可以查看 [Wiki](Wiki/README_ZH_CN.md)。

<br>

## 作者 [↑](#paldefender-幻兽帕鲁服务器反作弊)

- [Ultimeit](https://github.com/Ultimeit)
- [Zvendson](https://github.com/Zvendson)

<br>

## 致谢 [↑](#paldefender-幻兽帕鲁服务器反作弊)

* [Pocketpair, Inc.](https://www.pocketpair.jp/palworld)
* [Unreal Engine](https://www.unrealengine.com) - Epic Games

<br>

## 后记 [↑](#paldefender-幻兽帕鲁服务器反作弊)

**私たちは、[Pocketpair, Inc.](https://www.pocketpair.jp/palworld)による素晴らしい仕事に感謝の意を表したいと思います。色鮮やかな世界や、パルとのダイナミックなインタラクション、そして創造的なデザインは、チームの献身と情熱を見事に表しています。コミュニティの一員として、私たちはPalServer向けのプラグインを開発し、セキュリティを強化し、潜在的な悪用から守ることでPalworldをサポートしています**

**私たちは今後も、Palworldサーバーに最高水準のセキュリティと保護を提供できるよう努め続けます。皆様からのフィードバックは非常に貴重で、心から感謝しています。**<br>
~ [Zvend](https://github.com/Zvendson)

> *我们想向 [Pocketpair, Inc.](https://www.pocketpair.jp/palworld) 表达我们的感谢，感谢他们为幻兽帕鲁所做的非凡工作。色彩斑斓的世界、与帕鲁的动态互动以及创意设计都展示了团队的奉献精神和热情。作为社区的一员，我们也在为幻兽帕鲁开发服务端插件，增强安全性，并保护其免受潜在的漏洞攻击。*
<br><br>
*我们将继续努力，为您的幻兽帕鲁服务器提供最高水平的安全性和保护。您的反馈至关重要，我们由衷地感谢。*
