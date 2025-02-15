![PalDefender Logo](/.github/images/LOGO_WIKI.jpg)
*LOGO made by [Jia](<https://www.fiverr.com/javeriahjaved/design-a-unique-sports-mascot-esports-and-gaming-logo>)* !

# PalDefender Wiki

#### [English](./README.md) / 简体中文

## 目录

- [命令](./Commands/README_ZH_CN.md)
- [文件类型](./Files/README_ZH_CN.md)
- [数据列表](./Data%20Lists/README_ZH_CN.md)
- [常见问题解答](#faq)
  - [我不小心封禁了自己/别人。如何解除封禁？](#我不小心封禁了自己别人如何解除封禁)
  - [我无法以管理员身份登录，显示管理员命令被白名单保护。](#我无法以管理员身份登录显示管理员命令被白名单保护)
  - [我的服务器在启动时崩溃。](#我的服务器在启动时崩溃)
  - [我在服务器控制台中无法正确看到某些符号。](#我在服务器控制台中无法正确看到某些符号)
  - [如何报告崩溃？](#如何报告崩溃)

</details>

## 前言
此Wiki正在建设中，因此内容不完整。如果您能提供贡献或指出错误，将有助于Wiki逐步完善。

## 常见问题解答
### 我不小心封禁了自己/别人。如何解除封禁？
如果是封禁了他们的IP，您需要暂时编辑`Config.json`文件，并重新加载配置或重启服务器。如果是封禁了他们的账户，您需要从`Pal\Saved\SaveGames\banlist.txt`中删除他们的SteamID，并等待几分钟或在此之后重启服务器。

---

### 我无法以管理员身份登录，显示管理员命令被白名单保护。
确保您已将您的IP地址添加到`Config.json`文件中，如图所示。或者，您可以将`useAdminWhitelist`设置为`false`，但这不推荐，因为已知作弊者有某种漏洞能够获取管理员密码。

![AdminWhitelist](/.github/images/AdminWhitelist.png)

---

### 我的服务器在启动时崩溃。
请确保`Config.json`文件没有配置错误，尝试删除该文件并重新启动服务器。如果仍然无法解决问题，且这是您第一次使用PalDefender，建议安装[VC++ redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170)。

---

### 我在服务器控制台中无法正确看到某些符号。
请使用Windows Terminal（或任何支持Unicode的替代终端）代替默认的Windows控制台。

---

### 如何报告崩溃？
将`Pal\Saved\Crashes\*随机数字*\CrashContext.runtime-xml`文件 + 使用的PalDefender版本 + `Pal\Binaries\Win64\logs`文件夹中的日志发送至[issue section](https://github.com/Ultimeit/PalDefender/issues)的bug-reports频道。

---
