# :octicons-file-directory-16: 文件类型

**PalDefender** 支持多种自定义文件类型，可用于配置服务器行为并扩展功能。
当前支持：
* `Config.json`
* `WhiteList.json`
* `Banlist.json`
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json`
* `RESTAPI/RESTConfig.json`
* `RESTAPI/Tokens/*.json`

---

## :octicons-zap-16: 快速概览

### :octicons-tools-16: [Config.json](./Config.md)

控制服务器行为、管理规则、日志记录和管理员设置。

* **安全:** 反作弊（警告、踢出、封禁、IP 封禁）、名称/词语过滤、SteamID 保护、非法属性/物品检查。
* **日志:** 记录聊天、RCON、登录、死亡、召唤、建筑活动和油田事件。
* **管理员:** IP 白名单、自动登录、godmode/作弊命令、管理员操作可见性。
* **公告:** MOTD、玩家死亡、召唤、处罚和战利品事件。
* **聊天与玩法限制:** 消息长度、冷却绕过、PvP/PvE 伤害上限、砍树限制。
* **其他:** RCON base64 支持、启动失败处理、可选中文命令模式。

---

### :octicons-people-16: `WhiteList.json`

定义谁可以加入服务器。
同时支持 **User ID** 和 **IP 地址**（包括掩码范围）。

---

### :octicons-blocked-16: `Banlist.json`

存储 PalDefender 的封禁记录，供封禁、解封、IP 封禁和 REST 处罚工具使用。

* 优先使用 `/ban`、`/unban`、`/banip`、`/unbanip` 或 REST API，而不是手动编辑此文件。
* 如果必须手动编辑，请先停止服务器，或在修改后重新加载配置。

---

### :material-dna: [PalTemplate.json](./PalTemplate.md)

用于通过命令生成或发放自定义 Pals。

* 定义 Pal 的 **ID、昵称、性别、属性（HP/SP/MP）、饥饿值、SAN、闪光状态、技能、IV、被动**等内容。
* 允许完全自定义帕鲁的**战斗、功能和工作特性**。

---

### :octicons-location-16: [PalSummon.json](./PalSummon.md)

在指定位置生成自定义 Pal。

* 引用一个 `PalTemplate`，并设置**世界坐标（X、Y、Z）**。
* 配置**不可捕获**等标志，并禁用指定**状态效果**（例如中毒、溺水、燃烧等）。

---

### :octicons-list-unordered-16: [Pals/ImportRules/*.json](./PalImportRules.md)

控制自定义 Pal 模板如何被接受。

* 在 `Pals/ImportRules/Default.json` 中设置全局限制。
* 使用 `Pals/ImportRules/Anubis.json` 等文件添加单个 Pal 覆盖规则。
* 选择超过限制的数值是被阻止，还是被降低到上限。
* 选择被禁用的被动是阻止导入，还是在导入时移除。

---

### :octicons-globe-16: REST API 配置文件

REST API 配置位于 `RESTAPI/RESTConfig.json`，Bearer 令牌位于 `RESTAPI/Tokens/*.json`。

* `RESTConfig.json` 控制 API 是否启用、绑定地址、端口、控制台日志和 CORS 设置。
* 每个令牌文件应包含一个私有令牌和权限。不要公开分享令牌值。
