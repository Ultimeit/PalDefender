# 首页

![PalDefender Logo](../assets/LogoWiki.jpg)
<a href="https://discord.com/invite/bdTxPbwSEW" target="_blank">![Discord Server](https://img.shields.io/badge/-Join%20our%20Discord-111111?style=for-the-badge&logo=discord)</a>
<a href="https://www.nexusmods.com/palworld/mods/451" target="_blank">![Static Badge](https://img.shields.io/badge/-Nexus%20Mods-111111?style=for-the-badge&logo=nexusmods)</a>

<div style="display:flex; align-items:center; gap:12px;">

  <a href="https://ko-fi.com/T6T014OZZB" target="_blank">
    <img src="https://ko-fi.com/img/githubbutton_sm.svg" alt="Ko-fi">
  </a>

  <form action="https://www.paypal.com/donate" method="post" target="_top" style="margin:0;">
    <div id="donate-button-container">
      <div id="donate-button"></div>
      <script src="https://www.paypalobjects.com/donate/sdk/donate-sdk.js" charset="UTF-8"></script>
      <script>
        PayPal.Donation.Button({
          env: 'production',
          hosted_button_id: '6NVHHB52DSUZA',
          image: {
            src: 'https://www.paypalobjects.com/en_US/DK/i/btn/btn_donateCC_LG.gif',
            alt: 'Donate with PayPal button',
            title: 'PayPal - The safer, easier way to pay online!'
          }
        }).render('#donate-button');
      </script>
    </div>
  </form>

</div>

---

## 前言
本 Wiki 目前正在建设中，因此内容不完整。如果您能贡献内容或指出错误，我们将不胜感激，这样 Wiki 就能逐步完善。

代码是闭源的，我们没有开源的计划。

---

## 关于

PalDefender 实现了全面的服务器端验证，以防止各种已知和尚未发现的作弊、漏洞利用和崩溃。在执行任何玩家操作之前，PalDefender 都会检查潜在的作弊行为。根据服务器的配置，尝试此类操作的玩家会被警告、踢出、封禁或 IP 封禁。目前，此功能处于测试阶段，仅适用于基于 Windows 的专用服务器。

**欢迎有经验的 Linux 开发者帮助我们。**

---

## 作者

- <a href="https://github.com/Zvendson" target="_blank">Zvendson</a> (当前维护者)
- <a href="https://github.com/Ultimeit" target="_blank">Ultimeit</a> (原始创建者)
---

## 致谢

- <a href="https://www.pocketpair.jp/palworld" target="_blank">Pocketpair, Inc.</a>
- <a href="https://www.unrealengine.com" target="_blank">Unreal Engine</a> - Epic Games

---

## 后记

我们想对 <a href="https://www.pocketpair.jp/palworld" target="_blank">Pocketpair, Inc.</a> 在 Palworld 上的出色工作表示感谢。充满活力的世界、与帕鲁的动态互动以及富有创意的设计，都展现了团队的奉献精神和热情。作为社区的一员，我们也在通过为 PalServer 开发插件来支持 Palworld，该插件增强了安全性并保护其免受潜在的漏洞利用。

我们将继续努力为您的 Palworld 服务器提供最高水平的安全和保护。您的反馈非常宝贵，我们深表感谢。<br>
~ <a href="https://github.com/Zvendson" target="_blank">Zvend</a>
