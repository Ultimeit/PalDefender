# 命令

## 什么是命令？

命令是特殊的文本指令，可用于与游戏交互。在聊天中输入命令后，你可以执行传送、生成生物或管理玩家等操作。命令通常以 <span class="var-command">/</span> 开头，后面跟命令名称和可选参数。

## 谁可以使用命令？

**当前没有非管理员玩家可使用的命令。**
当前版本只提供管理员命令和 RCON 命令。

## 命令列表

!!! note "命令语法"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → 必须提供。<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → 可以省略。<span class="var-command-optional">{?}</span> 表示省略时使用的默认值。
    </p>
    <p>
    参数有不同类型，最常见的是 <span class="var-string">字符串</span>、<span class="var-number">数字</span>、<span class="var-float">浮点数</span> 和 <span class="var-bool">布尔值</span>。有些命令还使用更复杂的类型，例如特殊目录中的 <span class="file">文件名</span>，或一个 <span class="var-filter">过滤器</span>。
    </p>

!!! tip "ID 查询"
    使用 [paldeck.cc/pals](https://paldeck.cc/pals) 查询 `PalID`，[paldeck.cc/items](https://paldeck.cc/items) 查询 `ItemID`，[paldeck.cc/technology](https://paldeck.cc/technology) 查询 `TechID`，[paldeck.cc/buildings](https://paldeck.cc/buildings) 查询 `BuildingID`，[paldeck.cc/passives](https://paldeck.cc/passives) 查询 `PassiveID`，[paldeck.cc/skills](https://paldeck.cc/skills) 查询技能 ID。

??? note "仅 RCON"
    ??? info "/getrconcmds"
        **语法:** `/getrconcmds`

        **描述:** 返回 RCON 可用的所有命令及其所需参数数量。

        **参数:**

        - None

        **权限:** `RCON`

        **示例:**
        ```
        /getrconcmds
        ```

??? note "服务器管理"
    ??? info "/version"
        **语法:** `/version`

        **描述:** 显示 Palworld 游戏版本和 PalDefender 版本。RCON 返回 JSON 输出。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /version
        ```

    ??? info "/reloadcfg"
        **语法:** `/reloadcfg`

        **描述:** 重新加载 `Config.json`、`WhiteList.json` 和 PalDefender 封禁数据。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **语法:** `/addadminip <IP>`

        **描述:** 将 IP 地址添加到管理员白名单。

        **参数:**

        - `<IP>`: 要添加为管理员的 IP 地址。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **语法:** `/setadmin <UserId>`

        **描述:** 临时授予或撤销玩家的管理员权限。

        **参数:**

        - `<UserId>`: 要授予/撤销管理员权限的玩家 ID。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **语法:** `/pgbroadcast <Message>`

        **描述:** 向服务器上的所有玩家发送消息。

        **参数:**

        - `<Message>`: 要广播的消息。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /pgbroadcast "Server will restart soon."
        ```

    ??? info "/adminlogin"
        **语法:** `/adminlogin <password>`

        **描述:** 登录管理员模式。需要将管理员密码作为参数。

        **参数:**

        - `<password>`: 管理员密码。

        **权限:** `Chat`

        **示例:**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **语法:** `/adminlogout`

        **描述:** 退出管理员模式。

        **参数:**

        - None

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **语法:** `/iwantplayerlist`

        **描述:** 启用游戏内玩家列表叠加层，按 ESC 时可查看每名玩家的 UserId 和 Player UID。适合服务器管理员以及希望在游戏界面中直接查看详细玩家信息的玩家。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **语法:** `/getpos [UserId]`

        **描述:** 获取你当前的世界坐标，可用于传送、召唤等操作。如果提供 [UserId]，则获取该玩家的位置。

        **参数:**

        - `[UserId]`: （可选）要获取位置的玩家 ID。省略时获取你自己的位置。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **语法:** `/settime <hour>`

        **描述:** 更改 Palworld 中的时间。小时可为 `0` 到 `23`，也可以是 `day` 或 `night`。

        **参数:**

        - `<hour>`: 小时值（`0`–`23`、`day`、`night`）。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/togglepvp"
        **语法:** `/togglepvp`

        **描述:** 在当前运行会话中开启或关闭服务器 PvP。

        **参数:**

        - None

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /togglepvp
        ```

    ??? info "/alert"
        **语法:** `/alert <message>`

        **描述:** 向服务器上的所有玩家发送警报消息。该消息通常会醒目地显示在屏幕上。

        **参数:**

        - `<message>`: 要作为警报广播的消息。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /alert Server will restart in 5 minutes!
        ```

    ??? info "/send"
        **语法:** `/send <type> <UserId> <Message>`

        **描述:** 允许你向指定玩家发送消息或日志消息。

        **参数:**

        - `<type>`: 要发送的消息类型。可选值：
             - `msg`: 普通聊天消息。
             - `log`: 普通日志消息（白色、很快消失、较大字体）。
             - `ilog`: 重要日志消息（蓝色、显示时间较长）。
             - `vilog`: 非常重要的日志消息（蓝色、显示时间极长）。
        - `<UserId>`: 接收消息的玩家 ID。
        - `<Message>`: 要发送的消息文本。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /send msg steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send log steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send ilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send vilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        ```

    ??? info "/resetoilrig"
        **语法:** `/resetoilrig <lv30|lv55|lv60|all>`

        **描述:** 重置指定的 Oil Rig，或重置当前管理的全部 Oil Rig。

        **权限:** `Chat`，且必须处于游戏内管理员状态。

        **示例:**
        ```
        /resetoilrig all
        ```

    ??? info "/setting"
        **语法:** `/setting list [filter]` 或 `/setting <setting_name> <get|set|add|sub> [value]`

        **描述:** 检查或修改受支持的实时 `UPalGameSetting` 值。名称匹配不区分大小写，并接受唯一的前缀或子字符串。此功能仍处于实验阶段，不能替代持久化的世界配置，而且客户端可能继续显示缓存值。

        - `list [filter]`: 列出受支持的整数、浮点数、布尔值、字节和枚举字段。
        - `get`: 读取数值。
        - `set`: 设置任意受支持的类型。布尔值接受 `true/false`、`on/off`、`yes/no` 或 `1/0`；枚举接受数字或条目名称。
        - `add` / `sub`: 仅修改数值类型。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /setting list death
        /setting PalDeathPenaltyTime get
        /setting PalDeathPenaltyTime set 10
        ```

    ??? info "/resetbosstower"
        **语法:** `/resetbosstower <BossType|all>`

        **描述:** 仅限调试构建的命令，用于重置一个 Boss Tower 实例或所有可重置的 Boss Tower。指定单个目标时必须使用有效的 `EPalBossType` 名称。此命令不包含在公开的 Release 构建中。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /resetbosstower all
        ```

    ??? info "/showbosses"
        **语法:** `/showbosses`

        **描述:** 仅限调试构建的数据挖掘命令，将当前 Boss 静态信息写入 `PalDefender/Logs/BossInfo.json`。此命令不包含在公开的 Release 构建中。

        **权限:** `Chat`, `RCON`, `Admin`

??? note "基地管理"
    ??? info "/findunusedbases (别名: /findbases)"
        **语法:** `/findbases [empty|inactive|unused|all] [days=N] [builds<=N]`

        **交互语法:** `/findbases visit [filters]`、`/findbases next`、`/findbases kill [next]`

        **描述:** 扫描空置、不活跃或其他未使用的基地。`visit` 创建一个仅聊天可用的审核队列并传送到第一个结果；`next` 前往下一个；`kill` 摧毁选中的基地；`kill next` 摧毁后继续前往下一个。摧毁操作不可逆，因此请先检查每个目标。

        - `empty`: 没有工作帕鲁，且建筑数量不超过默认上限（或 `builds<=N`）。
        - `inactive`: 没有在线公会成员，且不活跃时间至少达到 `days`（默认 `30` 天）。
        - `unused`: 符合空置或不活跃条件。
        - `all`: 列出所有基地，同时仍应用明确指定的筛选条件。

        **权限:** 列表查询支持 `Chat` 和 `RCON`；visit/next/kill 需要游戏内聊天和管理员权限。

        **示例:**
        ```
        /findbases empty builds<=5
        /findbases inactive days=14
        /findbases visit unused days=30
        /findbases kill next
        ```
    ??? info "/getnearestbase"
        **语法:** `/getnearestbase [X] [Y] [Z]`

        **描述:** 显示离你角色最近的基地所属公会名称。

        **注意:** 通过 **RCON** 执行时必须提供全部位置参数（`[X]`、`[Y]`、`[Z]`），因为 RCON 没有可用于确定位置的玩家角色。

        **参数:**

        - `[X]`: （可选）X 坐标。
        - `[Y]`: （可选）Y 坐标。
        - `[Z]`: （可选）Z 坐标。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **语法:** `/gotonearestbase [X] [Y] [Z]`

        **描述:** 将你传送到当前位置附近最近的基地。

        **注意:** 通过 **RCON** 执行时必须提供全部位置参数（`[X]`、`[Y]`、`[Z]`），因为 RCON 没有可用于确定位置的玩家角色。

        **参数:**

        - `[X]`: （可选）X 坐标。
        - `[Y]`: （可选）Y 坐标。
        - `[Z]`: （可选）Z 坐标。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **语法:** `/killnearestbase [X] [Y] [Z]`

        **描述:** 摧毁最近的基地（**请谨慎使用！**）。

        **注意:** 通过 **RCON** 执行时必须提供全部位置参数（`[X]`、`[Y]`、`[Z]`），因为 RCON 没有可用于确定位置的玩家角色。

        **参数:**

        - `[X]`: （可选）X 坐标。
        - `[Y]`: （可选）Y 坐标。
        - `[Z]`: （可选）Z 坐标。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "玩家管理"
    ??? info "/kick"
        **语法:** `/kick <UserId> [Reason="Kicked by Admin."]`

        **描述:** 将玩家踢出服务器。

        **参数:**

        - `<UserId>`: 要踢出的玩家 ID。
        - `[Reason]`: （可选）踢出原因。默认："Kicked by Admin."

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /kick steam_76500000000000000 "Spamming in chat"
        ```

    ??? info "/ban"
        **语法:** `/ban <UserId> [Reason="Banned by Admin."]`

        **描述:** 封禁玩家并将其踢出服务器。

        **参数:**

        - `<UserId>`: 要封禁的玩家 ID。
        - `[Reason]`: （可选）封禁原因。默认："Banned by Admin."

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /ban gdk_25300000000000000 "Cheating"
        ```

    ??? info "/ipban"
        **语法:** `/ipban <UserId> [Reason="Banned by Admin."]`

        **描述:** 封禁玩家的 IP 地址，然后将其踢出服务器。

        **参数:**

        - `<UserId>`: 要进行 IP 封禁的玩家 ID。
        - `[Reason]`: （可选）封禁原因。默认："Banned by Admin."

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **语法:** `/banip <IP>`

        **描述:** 封禁一个 IP 地址。

        **参数:**

        - `<IP>`: 要封禁的 IP 地址。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **语法:** `/unbanip <IP>`

        **描述:** 从封禁列表中移除一个 IP 地址。

        **参数:**

        - `<IP>`: 要解除封禁的 IP 地址。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/unban"
        **语法:** `/unban <UserId> [Reason="Unbanned by admin."]`

        **描述:** 从 PalDefender 封禁列表中移除一个 UserId。

        **参数:**

        - `<UserId>`: 要解除封禁的 UserId。
        - `[Reason]`: （可选）为解除封禁操作保存的原因。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /unban steam_76500000000000000 "Appeal accepted"
        ```

    ??? info "/getip"
        **语法:** `/getip <UserId>`

        **描述:** 显示玩家的 IP 地址。

        **参数:**

        - `<UserId>`: 玩家的 ID。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **语法:** `/whitelist_add <UserId>`

        **描述:** 将 UserId 添加到白名单。

        **参数:**

        - `<UserId>`: 要加入白名单的玩家 ID。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **语法:** `/whitelist_remove <UserId>`

        **描述:** 从白名单中移除 UserId。

        **参数:**

        - `<UserId>`: 要从白名单移除的玩家 ID。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **语法:** `/whitelist_get`

        **描述:** 显示白名单玩家的完整列表。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **语法:** `/imcheater`

        **描述:** 用于测试服务器如何响应作弊者。

        **参数:**

        - None

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **语法:** `/spectate`

        **描述:** 开启旁观模式。效果与按下热键 `\` 相同，但该热键并非对所有人都有效，例如主机玩家。

        **参数:**

        - None

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /spectate
        ```

??? note "玩家角色"
    ??? info "/tp"
        **语法:**
        以下任一格式均可：

        - `/tp <UserId>`
        - `/tp <UserId1> <UserId2>`
        - `/tp <X> <Y>`
        - `/tp <X> <Y> <Z>`
        - `/tp <UserId> <X> <Y>`
        - `/tp <UserId> <X> <Y> <Z>`
        - `/tp home`
        - `/tp oilrig`
        - `/tp oilrig:Lv30`
        - `/tp oilrig:Lv55`
        - `/tp oilrig:Lv60`

        **描述:** 将你自己或指定玩家传送到另一名玩家、坐标、最近的己方基地或油田目标位置。

        **注意:** 使用 RCON 时必须指定要传送的玩家，因为 RCON 没有游戏内角色。

        **参数:**

        - `<UserId>`: 要传送到其身边的玩家；提供更多参数时，则表示要被传送的玩家。
        - `<UserId1>`: 要传送的玩家。
        - `<UserId2>`: 目标玩家。
        - `<X> <Y> [Z]`: 地图坐标。如果省略 `Z`，PalDefender 会尝试寻找可用的地面高度。
        - `home`: 传送到最近的自有基地。
        - `oilrig`、`oilrig:Lv30`、`oilrig:Lv55`、`oilrig:Lv60`: 传送到对应的 Oil Rig 目的地。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        /tp 100 -250
        /tp oilrig:Lv60
        ```

    ??? info "/give_exp"
        **语法:** `/give_exp <UserId> <Amount>`

        **描述:** 给玩家经验值。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<Amount>`: 经验值数量。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **语法:** `/giveme_exp <Amount>`

        **描述:** 给自己经验值。

        **参数:**

        - `<Amount>`: 经验值数量。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **语法:** `/renameplayer <UserId> <NewName>`

        **描述:** 修改玩家昵称。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<NewName>`: 新昵称。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /renameplayer steam_76500000000000000 NewNickname
        ```

    ??? info "/givestats"
        **语法:** `/givestats <UserId> [Count=1]`

        **描述:** 给玩家一个或多个未使用属性点；负数会扣除。不会影响已经分配的点数。

        **参数:**

        - `<UserId>`: 接收属性点的玩家 ID。
        - `[Count]`: （可选）给予的未使用属性点数量，可为负数以扣除。默认：1。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **语法:** `/givemestats [Count=1]`

        **描述:** 给自己一个或多个未使用属性点；负数会扣除。不会影响已经分配的点数。

        **参数:**

        - `[Count]`: （可选）给自己的未使用属性点数量，可为负数以扣除。默认：1。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **语法:** `/godmode [on/off]`

        **描述:** 授予无敌，包括免疫状态效果，阻止食物消耗，并在启用时恢复生命值。如果配置允许，也可以一击击杀所有目标。

        **参数:**

        - `[on/off]`: （可选）明确启用或禁用无敌模式。默认：切换开关。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

    ??? info "/admingun (别名: /agun)"
        **语法:** `/admingun`

        **描述:** 为当前游戏内管理员提供一把受保护的 Admin Gun。它可以立即击杀角色、摧毁地图物体、最大化植被伤害，拥有无限弹药和耐久度，并且不能丢弃、出售或移动到外部容器。蹲下摧毁储物对象时会删除其中内容；保持站立即可保留内容。该武器会在死亡、退出游戏或退出管理员状态时移除，再次领取会替换已有副本。

        **权限:** `Chat`，且必须处于游戏内管理员状态。不要求启用 `allowAdminCheats`。

        **示例:**
        ```
        /agun
        ```

??? note "公会管理"
    ??? info "/setguildleader"
        **语法:** `/setguildleader <UserId>`

        **描述:** 将目标玩家设为其当前公会的会长。

        **参数:**

        - `<UserId>`: 要设为公会会长的玩家 ID。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **语法:** `/exportguilds`

        **描述:** 将服务器上的所有公会导出到 Pal/Binaries/Win64/PalDefender/guildexport.json。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /exportguilds
        ```
        示例输出文件： `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "物品"
    ??? info "/give"
        **语法:** `/give <UserId> <ItemId> [Amount=1]`

        **描述:** 给玩家一个物品，并可指定数量。

        **参数:**

        - `<UserId>`: 接收物品的玩家 ID。
        - `<ItemId>`: 要给予的物品。
        - `[Amount]`: （可选）数量。默认：1。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **语法:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **描述:** 在一个命令中给玩家多个物品，可用冒号为每个物品指定数量。

        **参数:**

        - `<UserId>`: 接收物品的玩家 ID。
        - `<ItemId>[:<Amount>] ...`: 物品及其可选数量列表。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **语法:** `/giveme <ItemId> [Amount=1]`

        **描述:** 给自己一个物品，并可指定数量。

        **参数:**

        - `<ItemId>`: 要给自己的物品。
        - `[Amount]`: （可选）数量。默认：1。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **语法:** `/delitem <UserId> <ItemId> [Amount=1]`

        **描述:** 从玩家身上删除物品，并可指定数量。默认值为 `1`，只删除一个。使用 `all` 替代 `1` 可删除全部。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<ItemId>`: 要删除的物品。
        - `[Amount]`：（可选）数量。默认：1。使用 `all` 删除所有匹配项。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **语法:** `/give_relic <UserId> <RelicType> [Amount]`

        **描述:** 给玩家一个或多个指定类型的遗物点数。

        **参数:**

        - `<UserId>`: 接收遗物点数的玩家 ID。
        - `<RelicType>`: 要授予的遗物类型。

        - `[Amount]`: 可选的遗物点数数量，默认值为 `1`。

        **支持的遗物类型:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /give_relic steam_76500000000000000 CapturePower 5
        ```

    ??? info "/giveme_relic"
        **语法:** `/giveme_relic <RelicType> [Amount]`

        **描述:** 给自己一个或多个指定类型的遗物点数。

        **参数:**

        - `<RelicType>`: 要授予的遗物类型。

        - `[Amount]`: 给自己的可选遗物点数数量，默认值为 `1`。

        **支持的遗物类型:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /giveme_relic CapturePower 5
        ```


    ??? info "/delitems"
        **语法:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **描述:** 在一个命令中从玩家身上删除多个物品，可用冒号指定每种物品的数量。使用 `all` 替代 `1` 可删除全部。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<ItemId>[:<Amount>] ...`: 物品及其可选数量列表。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **语法:** `/clearinv <UserId> [Container=items] ...`

        **描述:** 清空玩家背包中的指定容器。可用容器包括 `items`、`keyitems`、`armor`、`weapons`、`food`、`dropslot` 或 `all`。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `[Container] ...`: （可选）要清空的容器。默认：items。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "帕鲁"
    ??? info "/givepal"
        **语法:** `/givepal <UserId> <PalId> [Level=1]`

        **描述:** 给玩家一只指定等级的帕鲁。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<PalId>`: 要给予的帕鲁。
            - **注意:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。
        - `[Level]`: （可选）Pal 等级。默认：1。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **语法:** `/givepal_j <UserID> <PalTemplate>`

        **描述:** 给玩家一只由 PalTemplate 文件定义的帕鲁。不再支持内嵌 JSON，只接受文件名。

        **注意:** 文件名不必包含 `.json` 扩展名；缺少时系统会自动添加。

        **参数:**

        - `<UserID>`: 玩家的 ID。
        - `<PalTemplate>`: PalTemplate 文件名（见 [PalTemplate](../FileTypes/PalTemplate.md)）。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **语法:** `/givemepal <PalId> [Level=1]`

        **描述:** 给自己一只指定等级的帕鲁。

        **参数:**

        - `<PalId>`: 要给自己的帕鲁。
            - **注意:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。
        - `[Level]`: （可选）Pal 等级。默认：1。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **语法:** `/givemepal_j <PalTemplate>`

        **描述:** 给自己一只由 PalTemplate 文件定义的帕鲁。不再支持内嵌 JSON，只接受文件名。

        **参数:**

        - `<PalTemplate>`: PalTemplate 文件名（见 [PalTemplate](../FileTypes/PalTemplate.md)）。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **语法:**
        以下任一格式均可：

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **描述:** 按相对或绝对坐标生成一只帕鲁。**RCON 必须指定 x、y 和 z！**

        **注意:** 除等级外，所有属性均随机生成。

        **参数:**
        - `<PalID>`: 要生成的帕鲁。
        - `[x]`: （可选）Pal 的 X 坐标。默认：相对于执行命令的玩家。
        - `[y]`: （可选）Pal 的 Y 坐标。默认：相对于执行命令的玩家。
        - `[z]`: （可选）Pal 的 Z 坐标。默认：相对于执行命令的玩家。
        - `[Level]`: （可选）Pal 等级。默认：1。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /spawnpal Anubis 255
        ```
        _生成一只 255 级的阿努比斯！_

    ??? info "/spawnnpc"
        **语法:** `/spawnnpc <NPCID|CharacterID> [Level=1]` 或 `/spawnnpc <NPCID|CharacterID> <X> <Y> [Z] [Level=1]`

        **描述:** 生成一个带 AI 的 NPC。在聊天中省略坐标时，会在管理员附近生成；RCON 必须提供坐标。仅提供 `X` 和 `Y` 时，PalDefender 会自动查找地面高度。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /spawnnpc PIDF_Soldier_AssaultRifle 30
        ```

    ??? info "/spawnpal_j"
        **语法:**

        以下任一格式均可：

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal_j <PalTemplate> [x] [y] [z]`

        **描述:** 按相对或绝对坐标生成一只帕鲁。**RCON 必须指定 x、y 和 z！**

        **注意:** 除等级外，所有属性均随机生成。

        **参数:**

        - `<PalTemplate>`: 要使用的 PalTemplate 文件名。
        - `[x]`: （可选）Pal 的 X 坐标。默认：相对于执行命令的玩家。
        - `[y]`: （可选）Pal 的 Y 坐标。默认：相对于执行命令的玩家。
        - `[z]`: （可选）Pal 的 Z 坐标。默认：相对于执行命令的玩家。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /spawnpal_j ArenaBoss 230 -486 4097
        ```

    ??? info "/summon"
        **语法:** `/summon <PalSummon>`

        **描述:** 使用指定的 PalSummon 文件生成帕鲁。

        **注意:** 文件名不必包含 `.json` 扩展名；缺少时系统会自动添加。

        **参数:**
        - `<PalSummon>`: 要使用的 PalSummon 文件名。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **语法:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **描述:** 给目标用户一个包含指定帕鲁的帕鲁蛋，并可选择调整等级。

        **参数:**

        ??? quote "<UserId\>"
            **描述:** 接收帕鲁蛋的玩家 ID。

        ??? quote "<EggId\>"
            **描述:** 要给予的蛋类型。

            **注意:** 每种类型允许使用 01（最小）到 05（最大）的值：

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **描述:** 蛋中包含的帕鲁。

            **注意:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。

        ??? quote "[Level\]"
            **描述:** （可选）蛋中帕鲁的等级。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **语法:** `/givemeegg <EggId> <PalId> [Level]`

        **描述:** 给自己一个包含指定帕鲁的帕鲁蛋，并可选择调整等级。

        **参数:**

        ??? quote "<EggId\>"
            **描述:** 要给自己的蛋类型。

            **注意:** 每种类型允许使用 01（最小）到 05（最大）的值：

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **描述:** 蛋中包含的帕鲁。

            **注意:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。

        ??? quote "[Level]"
            **描述:** （可选）蛋中帕鲁的等级。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **语法:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **描述:** 给出一个帕鲁蛋，内部帕鲁由 PalTemplate 文件定义，并可选择调整等级。

        **参数:**

        ??? quote "<EggId\>"
            **描述:** 要给予的蛋类型。

            **注意:** 每种类型允许使用 01（最小）到 05（最大）的值：

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **描述:** 要使用的 PalTemplate 文件名。

            **注意：** 文件名不需要包含 .json 扩展名；如果缺失，系统会自动追加。参见 [PalTemplate](../FileTypes/PalTemplate.md)。

        ??? quote "[Level]"
            **描述:** （可选）蛋中帕鲁的等级。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **语法:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **描述:** 给自己一个帕鲁蛋，内部帕鲁由 PalTemplate 文件定义，并可选择调整等级。

        **参数:**

        ??? quote "<EggI\>"
            **描述:** 要给自己的蛋类型。

            **注意:** 每种类型允许使用 01（最小）到 05（最大）的值：

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **描述:** 要使用的 PalTemplate 文件名。

            **注意：** 文件名不需要包含 .json 扩展名；如果缺失，系统会自动追加。参见 [PalTemplate](../FileTypes/PalTemplate.md)。

        ??? quote "[Level]"
            **描述:** （可选）蛋中帕鲁的等级。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **语法:** `/jetragon`

        **描述:** 给你一只管理员空涡龙帕鲁（它飞得太快了……）。

        **参数:**
        - None

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **语法:** `/catwaifu`

        **描述:** 给你一只管理员猫娘帕鲁，用于增强角色属性。

        **参数:**

        - None

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **语法:** `/exportpals [UserId]`

        **描述:** 将玩家的每只帕鲁导出为 PalTemplate 文件，位置为 Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/。

        **参数:**

        - `[UserId]`: （可选）要导出帕鲁的玩家 ID。省略时导出你自己的帕鲁。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **语法:** `/deletepals <UserId> <PalFilter>`

        **描述:** 使用高级过滤器删除指定用户的帕鲁。过滤器允许在一个命令中指定多个条件，例如 Pal ID、等级、性别、被动技能等。用于重要数据前请先在安全环境中测试。

        **参数:**

        ??? quote "<UserId\>"
            **描述:** 其帕鲁将被删除的玩家 ID。

        ??? quote "<PalFilter\>"
            **描述:** 用于选择要删除哪些帕鲁的一组过滤关键字。

            **注意:** 一条命令中可以组合多个关键字。

        可用的筛选关键字：

            - `ID`: PalID or list of PalIDs (comma-separated)
            - `Nick`: 字符串（帕鲁名称）
            - `Gender`: `male` or `female`
            - `Level`: 数字，支持 `<`、`>`、`<=`、`>=`、`=`、`!=`
            - `Rank`: 数字，支持 `<`、`>`、`<=`、`>=`、`=`、`!=`
            - `Lucky`: `true` or `false` (shiny)
            - `Passives`: PassiveSkill or list of PassiveSkills (comma-separated)
            - `Limit`: 数字（最多删除的帕鲁数量）

            **示例过滤器：**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            上述筛选键和示例即为当前的 PalFilter 参考。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "科技树"
    ??? info "/learntech"
        **语法:** `/learntech <UserId> <TechID>`

        **描述:** 让玩家学习指定科技。使用 `all` 可解锁全部。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<TechID>`: 要学习的科技。使用 `all` 解锁全部。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **语法:** `/unlearntech <UserId> <TechID>`

        **描述:** 让玩家遗忘指定科技。使用 `all` 可移除全部。

        **参数:**

        - `<UserId>`: 玩家的 ID。
        - `<TechID>`: 要遗忘的科技。使用 `all` 移除全部。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **语法:** `/givetechpoints <UserId> [Amount=1]`

        **描述:** 给目标用户 X 点科技点。

        **参数:**

        - `<UserId>`: 接收科技点的玩家 ID。
        - `[Amount]`: （可选）给予的科技点数量。默认：1。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **语法:** `/givebosstechpoints <UserId> [Amount=1]`

        **描述:** 给目标用户 X 点古代科技点。

        **参数:**

        - `<UserId>`: 接收古代科技点的玩家 ID。
        - `[Amount]`: （可选）给予的古代科技点数量。默认：1。

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **语法:** `/givemetechpoints [Amount=1]`

        **描述:** 给自己 X 点科技点。

        **参数:**

        - `[Amount]`: （可选）给自己的科技点数量。默认：1。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **语法:** `/givemebosstechpoints [Amount=1]`

        **描述:** 给自己 X 点古代科技点。

        **参数:**

        - `[Amount]`: （可选）给自己的古代科技点数量。默认：1。

        **权限:** `Chat`, `Admin`

        **示例:**
        ```
        /givemebosstechpoints 5
        ```


??? note "数据挖掘"
    ??? info "/gettechids"
        **语法:** `/gettechids`

        **描述:** 返回所有可用科技 ID 的列表。RCON 会得到 JSON 输出。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **语法:** `/getskinids`

        **描述:** 返回所有可用帕鲁皮肤 ID 的列表。RCON 会得到 JSON 输出。

        **参数:**

        - None

        **权限:** `Chat`, `RCON`, `Admin`

        **示例:**
        ```
        /getskinids
        ```
