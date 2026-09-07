# 功能与当前状态

本页概述 PalDefender 1.9.1 中面向用户的功能开关。准确的默认值请参阅 [`Config.json`](./FileTypes/Config.md)。

## 当前启用的防护

- 伤害、耐力、弹药和基地复制检测可以分别开关。
- Anti-Vacuum 会阻止对普通物品、Pal 蛋、遗物和笔记的可疑远距离拾取。启用 `allowAdminCheats` 时，管理员可以绕过受支持的检查。
- 无效物品、Pal 属性、工作台配方、Doctor Surgi、紧急重生以及其他服务器操作检查仍属于中央验证层。
- `BannedCampWorker` 会阻止配置的 Character ID 被分配到基地。

由 `antiDupe...` 键控制的旧功能在当前发布版本中已被编译禁用。新的基地复制检测是独立功能，由 `baseCampDupeDetectionEnabled` 控制。

## 管理与事件

- `/admingun`（`/agun`）向已登录的管理员发放受保护的 [Admin Gun](./Commands/index.md)。
- `/setting` 可以查看或临时修改受支持的 Palworld 实时设置。
- `/findbases` 提供用于检查空置或不活跃基地的交互式队列。
- PalSummon 支持遭遇名称、AI/伤害统计控制、属性倍率、条件捕获、排名结果和可配置奖励。请参阅 [`PalSummon.json`](./FileTypes/PalSummon.md)。
- Discord 目标在 `PalWebhooks` 中配置，涵盖聊天、命令、死亡、加入/离开、召唤、Oil Rig 事件和反作弊检测。

## Heartbeat

Release 构建会在游戏就绪后每 10 秒向 `https://pallink.net/api/heartbeat` 发送 heartbeat。Payload 包含世界/服务器 GUID、操作系统区域国家代码、PalDefender 和 Palworld 版本、Windows/Wine/Proton 平台、进程运行时间，以及在线、最大和累计唯一玩家数量。它不包含玩家姓名、玩家账号 ID、玩家 IP 地址、聊天消息或存档内容。Debug 构建不发送 heartbeat。

## REST API

经过身份验证的 REST API 支持玩家、Pal、物品栏、科技、进度、公会、封禁、消息、奖励和管理操作。1.9.0 还新增了 [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) 和 [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md)。
