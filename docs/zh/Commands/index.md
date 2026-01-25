# 命令

## 什么是命令？

命令是特殊的基于文本的指令，允许您与游戏交互。通过在聊天中输入命令，您可以执行传送、生成生物或管理玩家等操作。命令通常以 <span class="var-command">/</span> 开头，后跟命令名称和可选参数。

## 谁可以使用命令？

**目前没有非管理员玩家可以使用的命令。**
在当前版本中，只有管理员和 RCON 命令可用。

## 命令列表

!!! note "命令语法"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → 必须包含。<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → 可以省略。<span class="var-command-optional">{?}</span> 表示省略时使用的默认值。
    </p>
    <p>
    参数有不同的类型。最常见的是 <span class="var-string">字符串</span>、<span class="var-number">数字</span>、<span class="var-float">浮点数</span> 和 <span class="var-bool">布尔值</span>。某些命令甚至具有复杂类型，例如特殊目录中的特定 <span class="file">文件名</span> 或实际上是 <span class="var-filter">过滤器</span>。
    </p>

??? note "仅 RCON"
    ??? info "/getrconcmds"
        **语法：** `/getrconcmds`

        **描述：** 返回 RCON 可用的每个命令及其所需参数数量的列表。

        **参数：**

        - 无

        **权限：** `RCON`

        **示例：**
        ```
        /getrconcmds
        ```

??? note "服务器管理"
    ??? info "/reloadcfg"
        **语法：** `/reloadcfg`

        **描述：** 重新加载 `Config.json`、`whitelist.json` 和 `banlist.txt`。

        **参数：**

        - 无

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **语法：** `/addadminip <IP>`

        **描述：** 将 IP 地址添加到管理员白名单。

        **参数：**

        - `<IP>`：要添加为管理员的 IP 地址。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **语法：** `/setadmin <UserId>`

        **描述：** 临时授予/撤销玩家的管理员权限。

        **参数：**

        - `<UserId>`：要授予/撤销管理员权限的玩家 ID。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **语法：** `/pgbroadcast <Message>`

        **描述：** 向服务器中的所有玩家发送消息。

        **参数：**

        - `<Message>`：要广播的消息。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /pgbroadcast "服务器即将重启。"
        ```

    ??? info "/adminlogin"
        **语法：** `/adminlogin <password>`

        **描述：** 将您登录到管理员模式。需要您的管理员密码作为参数。

        **参数：**

        - `<password>`：管理员密码。

        **权限：** `Chat`

        **示例：**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **语法：** `/adminlogout`

        **描述：** 将您从管理员模式登出。

        **参数：**

        - 无

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **语法：** `/iwantplayerlist`

        **描述：** 启用游戏内玩家列表覆盖层，允许您在按 ESC 时查看每个玩家的 UserId 和 Player UID。对于想要直接在游戏界面中查看详细玩家信息的服务器管理员和玩家很有用。

        **参数：**

        - 无

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **语法：** `/getpos [UserId]`

        **描述：** 获取您在世界中的当前位置，可用于传送、召唤和类似操作。如果提供了 [UserId]，则获取该玩家的位置。

        **参数：**

        - `[UserId]`：（可选）要获取位置的玩家 ID。如果省略，则获取您自己的位置。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **语法：** `/settime <hour>`

        **描述：** 更改 Palworld 中的时间。小时可以有以下值：`0` 到 `23`、`day` 和 `night`。

        **参数：**

        - `<hour>`：小时值（0-23、day、night）。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/alert"
        **语法：** `/alert <message>`

        **描述：** 向服务器上的所有玩家发送警报消息。此消息通常会在他们的屏幕上显著显示。

        **参数：**

        - `<message>`：要作为警报广播的消息。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /alert 服务器将在 5 分钟后重启！
        ```

    ??? info "/send"
        **语法：** `/send <type> <UserId> <Message>`

        **描述：** 允许您向特定玩家发送消息或日志消息。

        **参数：**

        - `<type>`：要发送的消息类型。可能的值：
             - `msg`：常规聊天消息。
             - `log`：常规日志消息（白色，快速消失，较大字体）。
             - `ilog`：重要日志消息（蓝色，停留时间更长）。
             - `vilog`：非常重要的日志消息（蓝色，停留时间极长）。
        - `<UserId>`：接收消息的玩家 ID。
        - `<Message>`：要发送的消息文本。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /send msg steam_76500000000000000 不要错过 Qonzer 的促销活动！
        /send log steam_76500000000000000 不要错过 Qonzer 的促销活动！
        /send ilog steam_76500000000000000 不要错过 Qonzer 的促销活动！
        /send vilog steam_76500000000000000 不要错过 Qonzer 的促销活动！
        ```

??? note "基地管理"
    ??? info "/getnearestbase"
        **语法：** `/getnearestbase [X] [Y] [Z]`

        **描述：** 告诉您拥有距离您角色最近基地的公会名称。

        **注意：** 通过 **RCON** 执行时，所有位置参数（`[X]` `[Y]` `[Z]`）**都是必需的**，因为 RCON 没有玩家角色来确定位置。

        **参数：**

        - `[X]`：（可选）X 坐标。
        - `[Y]`：（可选）Y 坐标。
        - `[Z]`：（可选）Z 坐标。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **语法：** `/gotonearestbase [X] [Y] [Z]`

        **描述：** 将您传送到该位置最近的基地。

        **注意：** 通过 **RCON** 执行时，所有位置参数（`[X]` `[Y]` `[Z]`）**都是必需的**，因为 RCON 没有玩家角色来确定位置。

        **参数：**

        - `[X]`：（可选）X 坐标。
        - `[Y]`：（可选）Y 坐标。
        - `[Z]`：（可选）Z 坐标。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **语法：** `/killnearestbase [X] [Y] [Z]`

        **描述：** 摧毁最近的基地（**请谨慎使用！**）。

        **注意：** 通过 **RCON** 执行时，所有位置参数（`[X]` `[Y]` `[Z]`）**都是必需的**，因为 RCON 没有玩家角色来确定位置。

        **参数：**

        - `[X]`：（可选）X 坐标。
        - `[Y]`：（可选）Y 坐标。
        - `[Z]`：（可选）Z 坐标。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /killnearestbase 100 200 50
        ```


??? note "玩家管理"
    ??? info "/kick"
        **语法：** `/kick <UserId> [Reason="Kicked by Admin."]`

        **描述：** 将玩家从服务器踢出。

        **参数：**

        - `<UserId>`：要踢出的玩家 ID。
        - `[Reason]`：（可选）踢出原因。默认："Kicked by Admin."

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /kick steam_76500000000000000 "在聊天中刷屏"
        ```

    ??? info "/ban"
        **语法：** `/ban <UserId> [Reason="Banned by Admin."]`

        **描述：** 封禁并踢出服务器中的玩家。

        **参数：**

        - `<UserId>`：要封禁的玩家 ID。
        - `[Reason]`：（可选）封禁原因。默认："Banned by Admin."

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /ban gdk_25300000000000000 "作弊"
        ```

    ??? info "/ipban"
        **语法：** `/ipban <UserId> [Reason="Banned by Admin."]`

        **描述：** 封禁玩家的 IP 地址，然后将其从服务器踢出。

        **参数：**

        - `<UserId>`：要 IP 封禁的玩家 ID。
        - `[Reason]`：（可选）封禁原因。默认："Banned by Admin."

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **语法：** `/banip <IP>`

        **描述：** 从服务器封禁 IP 地址。

        **参数：**

        - `<IP>`：要封禁的 IP 地址。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **语法：** `/unbanip <IP>`

        **描述：** 从封禁列表中移除 IP 地址。

        **参数：**

        - `<IP>`：要解封的 IP 地址。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/getip"
        **语法：** `/getip <UserId>`

        **描述：** 显示玩家的 IP 地址。

        **参数：**

        - `<UserId>`：玩家 ID。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **语法：** `/whitelist_add <UserId>`

        **描述：** 将 UserId 添加到白名单。

        **参数：**

        - `<UserId>`：要添加到白名单的玩家 ID。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **语法：** `/whitelist_remove <UserId>`

        **描述：** 从白名单中移除 UserId。

        **参数：**

        - `<UserId>`：要从白名单中移除的玩家 ID。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **语法：** `/whitelist_get`

        **描述：** 显示白名单玩家的完整列表。

        **参数：**

        - 无

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **语法：** `/imcheater`

        **描述：** 使用此命令测试服务器对作弊者的响应。

        **参数：**

        - 无

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **语法：** `/spectate`

        **描述：** 开启观察者模式。与按快捷键 `\` 相同，但快捷键对某些人不起作用，比如主机玩家。

        **参数：**

        - 无

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /spectate
        ```

??? note "玩家角色"
    ??? info "/tp"
        **语法：** `/tp <UserId1> <UserId2>`

        **描述：** 将 UserId1 传送到 UserId2。

        **参数：**

        - `<UserId1>`：要传送的玩家。
        - `<UserId2>`：目标玩家。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        ```

    ??? info "/give_exp"
        **语法：** `/give_exp <UserId> <Amount>`

        **描述：** 给予玩家经验值。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<Amount>`：经验值数量。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **语法：** `/giveme_exp <Amount>`

        **描述：** 给予自己经验值。

        **参数：**

        - `<Amount>`：经验值数量。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **语法：** `/renameplayer <UserId> <NewName>`

        **描述：** 重命名玩家的昵称。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<NewName>`：新昵称。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /renameplayer steam_76500000000000000 NewNickname
        ```

    ??? info "/givestats"
        **语法：** `/givestats <UserId> [Count=1]`

        **描述：** 给予玩家一个或多个未使用的属性点（负值将减少）。不影响已使用的点数。

        **参数：**

        - `<UserId>`：接收属性点的玩家 ID。
        - `[Count]`：（可选）要给予的未使用属性点数量（可以为负数以减少）。默认：1。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **语法：** `/givemestats [Count=1]`

        **描述：** 给予自己一个或多个未使用的属性点（负值将减少）。不影响已使用的点数。

        **参数：**

        - `[Count]`：（可选）要给予自己的未使用属性点数量（可以为负数以减少）。默认：1。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **语法：** `/godmode [on/off]`

        **描述：** 授予无敌状态，包括状态效果免疫，拒绝消耗食物并在激活时恢复生命值。如果在配置中启用，可选择允许一击必杀所有东西。

        **参数：**

        - `[on/off]`：（可选）明确启用或禁用无敌模式。默认：切换开关。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

??? note "公会管理"
    ??? info "/setguildleader"
        **语法：** `/setguildleader <UserId>`

        **描述：** 使目标玩家成为其当前公会的领导者。

        **参数：**

        - `<UserId>`：要设为公会领导者的玩家 ID。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **语法：** `/exportguilds`

        **描述：** 将服务器的每个公会转储到 Pal/Binaries/Win64/PalDefender/guildexport.json。

        **参数：**

        - 无

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /exportguilds
        ```
        示例输出文件：`Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "物品"
    ??? info "/give"
        **语法：** `/give <UserId> <ItemId> [Amount=1]`

        **描述：** 给予玩家一个物品，如果指定了数量则给予相应数量。

        **参数：**

        - `<UserId>`：要给予物品的玩家 ID。
        - `<ItemId>`：要给予的物品。
        - `[Amount]`：（可选）数量。默认：1。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **语法：** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **描述：** 在一个命令中给予玩家多个物品，如果指定了数量则用冒号分隔每个物品的数量。

        **参数：**

        - `<UserId>`：要给予物品的玩家 ID。
        - `<ItemId>[:<Amount>] ...`：物品列表和可选数量。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **语法：** `/giveme <ItemId> [Amount=1]`

        **描述：** 给予自己一个物品，如果指定了数量则给予相应数量。

        **参数：**

        - `<ItemId>`：要给予自己的物品。
        - `[Amount]`：（可选）数量。默认：1。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **语法：** `/delitem <UserId> <ItemId> [Amount=1]`

        **描述：** 从玩家处删除一个物品，如果指定了数量则删除相应数量。默认为 `1`，只会删除该物品的 1 个实例。使用 `all` 代替 `1` 以删除所有实例。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<ItemId>`：要删除的物品。
        - `[Amount]`：（可选）数量。默认：1。使用 `all` 删除所有实例。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **语法：** `/give_relic <UserId> <Amount>`

        **描述：** 给予玩家一个或多个利弗蒙克雕像。

        **参数：**

        - `<UserId>`：接收利弗蒙克雕像的玩家 ID。
        - `<Amount>`：要给予的利弗蒙克雕像数量。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /give_relic steam_76500000000000000 5
        ```

    ??? info "/giveme_relic"
        **语法：** `/giveme_relic <Amount>`

        **描述：** 给予自己一个或多个利弗蒙克雕像。

        **参数：**

        - `<Amount>`：要给予自己的利弗蒙克雕像数量。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /giveme_relic 5
        ```


    ??? info "/delitems"
        **语法：** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **描述：** 在一个命令中从玩家处删除多个物品，如果指定了数量则用冒号分隔每个物品的数量。使用 `all` 代替 `1` 以删除所有实例。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<ItemId>[:<Amount>] ...`：物品列表和可选数量。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **语法：** `/clearinv <UserId> [Container=items] ...`

        **描述：** 清除玩家库存中的指定容器。可用容器：`items`、`keyitems`、`armor`、`weapons`、`food`、`dropslot` 或 `all`。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `[Container] ...`：（可选）要清除的容器。默认：items。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "帕鲁"
    ??? info "/givepal"
        **语法：** `/givepal <UserId> <PalId> [Level=1]`

        **描述：** 在指定等级给予玩家一个帕鲁。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<PalId>`：要给予的帕鲁。
            - **注意：** 使用帕鲁的开发者名称，例如 `WeaselDragon`（滑水蛇）。完整列表请参见 [paldeck.cc/pals](https://paldeck.cc/pals)。
        - `[Level]`：（可选）帕鲁等级。默认：1。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **语法：** `/givepal_j <UserID> <PalTemplate>`

        **描述：** 给予玩家一个由 PalTemplate 文件定义的帕鲁。不再支持嵌入式 JSON；仅接受文件名。

        **注意：** 您不需要在文件名中包含 .json 扩展名；如果缺少，系统会自动添加。

        **参数：**

        - `<UserID>`：玩家 ID。
        - `<PalTemplate>`：PalTemplate 文件的名称（参见 [PalTemplate](/FileTypes/PalTemplate)）。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **语法：** `/givemepal <PalId> [Level=1]`

        **描述：** 在指定等级给予自己一个帕鲁。

        **参数：**

        - `<PalId>`：要给予自己的帕鲁。
            - **注意：** 使用帕鲁的开发者名称，例如 `WeaselDragon`（滑水蛇）。完整列表请参见 [paldeck.cc/pals](https://paldeck.cc/pals)。
        - `[Level]`：（可选）帕鲁等级。默认：1。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **语法：** `/givemepal_j <PalTemplate>`

        **描述：** 给予自己一个由 PalTemplate 文件定义的帕鲁。不再支持嵌入式 JSON；仅接受文件名。

        **参数：**

        - `<PalTemplate>`：PalTemplate 文件的名称（参见 [PalTemplate](/FileTypes/PalTemplate)）。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **语法：**
        以下任一形式都可以：

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **描述：** 在您附近或绝对位置生成一个帕鲁。**RCON 必须指定 x、y 和 z！**

        **注意：** 除等级外，所有属性都是随机的。

        **参数：**
        - `<PalID>`：要生成的帕鲁。
        - `[x]`：（可选）帕鲁的 x 位置。默认：相对于调用玩家。
        - `[y]`：（可选）帕鲁的 y 位置。默认：相对于调用玩家。
        - `[z]`：（可选）帕鲁的 z 位置。默认：相对于调用玩家。
        - `[Level]`：（可选）帕鲁等级。默认：1。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /spawnpal Anubis 255
        ```
        _生成一个等级为 255 的阿努比斯！_

    ??? info "/spawnpal_j"
        **语法：**

        以下任一形式都可以：

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal <PalTemplate> [x] [y] [z]`

        **描述：** 在您附近或绝对位置生成一个帕鲁。**RCON 必须指定 x、y 和 z！**

        **注意：** 除等级外，所有属性都是随机的。

        **参数：**

        - `<PalTemplate>`：要使用的 PalTemplate 文件名。
        - `[x]`：（可选）帕鲁的 x 位置。默认：相对于调用玩家。
        - `[y]`：（可选）帕鲁的 y 位置。默认：相对于调用玩家。
        - `[z]`：（可选）帕鲁的 z 位置。默认：相对于调用玩家。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /spawnpal Anubis 255
        ```
        _生成一个等级为 255 的阿努比斯！_

    ??? info "/summon"
        **语法：** `/summon <PalSummon>`

        **描述：** 使用提供的 PalSummon 文件生成一个帕鲁。

        **注意：** 您不需要在文件名中包含 .json 扩展名；如果缺少，系统会自动添加。

        **参数：**
        - `<PalSummon>`：要使用的 PalSummon 文件名。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **语法：** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **描述：** 给予目标用户一个包含特定帕鲁的帕鲁蛋，可选择调整等级。

        **参数：**

        ??? quote "<UserId\>"
            **描述：** 接收蛋的玩家 ID。

        ??? quote "<EggId\>"
            **描述：** 要给予的蛋类型。

            **注意：** 每种类型允许的值从 01（最小）到 05（最大）：

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
            **描述：** 蛋内的帕鲁。

            **注意：** 使用帕鲁的开发者名称，例如 `WeaselDragon`（滑水蛇）。完整列表请参见 [paldeck.cc/pals](https://paldeck.cc/pals)。

        ??? quote "[Level\]"
            **描述：** （可选）蛋内帕鲁的等级。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **语法：** `/givemeegg <EggId> <PalId> [Level]`

        **描述：** 给予自己一个包含特定帕鲁的帕鲁蛋，可选择调整等级。

        **参数：**

        ??? quote "<EggId\>"
            **描述：** 要给予自己的蛋类型。

            **注意：** 每种类型允许的值从 01（最小）到 05（最大）：

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
            **描述：** 蛋内的帕鲁。

            **注意：** 使用帕鲁的开发者名称，例如 `WeaselDragon`（滑水蛇）。完整列表请参见 [paldeck.cc/pals](https://paldeck.cc/pals)。

        ??? quote "[Level]"
            **描述：** （可选）蛋内帕鲁的等级。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **语法：** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **描述：** 给予一个包含由 PalTemplate 文件定义的帕鲁的帕鲁蛋，可选择调整等级。

        **参数：**

        ??? quote "<EggId\>"
            **描述：** 要给予的蛋类型。

            **注意：** 每种类型允许的值从 01（最小）到 05（最大）：

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
            **描述：** 要使用的 PalTemplate 文件名。

            **注意：** 您不需要在文件名中包含 .json 扩展名；如果缺少，系统会自动添加。参见 [PalTemplate](/FileTypes/PalTemplate)。

        ??? quote "[Level]"
            **描述：** （可选）蛋内帕鲁的等级。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **语法：** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **描述：** 给予自己一个包含由 PalTemplate 文件定义的帕鲁的帕鲁蛋，可选择调整等级。

        **参数：**

        ??? quote "<EggId\>"
            **描述：** 要给予自己的蛋类型。

            **注意：** 每种类型允许的值从 01（最小）到 05（最大）：

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
            **描述：** 要使用的 PalTemplate 文件名。

            **注意：** 您不需要在文件名中包含 .json 扩展名；如果缺少，系统会自动添加。参见 [PalTemplate](/FileTypes/PalTemplate)。

        ??? quote "[Level]"
            **描述：** （可选）蛋内帕鲁的等级。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **语法：** `/jetragon`

        **描述：** 给予您一个管理员-喷气龙帕鲁（它飞得...很快）。

        **参数：**
        - 无

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **语法：** `/catwaifu`

        **描述：** 给予您一个管理员-猫娘，可以增强您的角色属性。

        **参数：**

        - 无

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **语法：** `/exportpals [UserId]`

        **描述：** 将玩家的每个帕鲁导出到 Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/ 的 PalTemplate 文件。

        **参数：**

        - `[UserId]`：（可选）要导出帕鲁的玩家 ID。如果省略，则导出您自己的帕鲁。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **语法：** `/deletepals <UserId> <PalFilter>`

        **描述：** 使用高级过滤器从指定用户删除帕鲁。过滤器允许您在一个命令中指定多个条件（例如帕鲁 ID、等级、性别、被动技能等）。请在使用重要数据之前在安全环境中测试。

        **参数：**

        ??? quote "<UserId\>"
            **描述：** 要删除帕鲁的玩家 ID。

        ??? quote "<PalFilter\>"
            **描述：** 用于选择要删除的帕鲁的过滤器关键字集合。

            **注意：** 可以在一个命令中组合多个关键字。

            可用过滤器关键字：

            - `ID`：PalID 或 PalID 列表（逗号分隔）
            - `Nick`：字符串（帕鲁名称）
            - `Gender`：`male` 或 `female`
            - `Level`：数字，支持符号 `<`、`>`、`<=`、`>=`、`=`、`!=`
            - `Rank`：数字，支持符号 `<`、`>`、`<=`、`>=`、`=`、`!=`
            - `Lucky`：`true` 或 `false`（闪光）
            - `Passives`：PassiveSkill 或 PassiveSkill 列表（逗号分隔）
            - `Limit`：数字（要删除的最大帕鲁数量）

            **示例过滤器：**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            更多详细信息，请参见 [PalFilter 文档](https://github.com/Ultimeit/PalDefender/blob/beta/Wiki/Commands/deletepals.md)。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "研究树"
    ??? info "/learntech"
        **语法：** `/learntech <UserId> <TechID>`

        **描述：** 让玩家学习特定技术。使用 `all` 解锁所有内容。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<TechID>`：要学习的技术。使用 `all` 解锁所有内容。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **语法：** `/unlearntech <UserId> <TechID>`

        **描述：** 让玩家忘记特定技术。使用 `all` 移除所有内容。

        **参数：**

        - `<UserId>`：玩家 ID。
        - `<TechID>`：要忘记的技术。使用 `all` 移除所有内容。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **语法：** `/givetechpoints <UserId> <Amount>`

        **描述：** 给予目标用户 X 个技术点数。

        **参数：**

        - `<UserId>`：接收技术点数的玩家 ID。
        - `<Amount>`：要给予的技术点数数量。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **语法：** `/givebosstechpoints <UserId> <Amount>`

        **描述：** 给予目标用户 X 个古代技术点数。

        **参数：**

        - `<UserId>`：接收古代技术点数的玩家 ID。
        - `<Amount>`：要给予的古代技术点数数量。

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **语法：** `/givemetechpoints <Amount>`

        **描述：** 给予自己 X 个技术点数。

        **参数：**

        - `<Amount>`：要给予自己的技术点数数量。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **语法：** `/givemebosstechpoints <Amount>`

        **描述：** 给予自己 X 个古代技术点数。

        **参数：**

        - `<Amount>`：要给予自己的古代技术点数数量。

        **权限：** `Chat`、`Admin`

        **示例：**
        ```
        /givemebosstechpoints 5
        ```


??? note "数据挖掘"
    ??? info "/gettechids"
        **语法：** `/gettechids`

        **描述：** 返回所有可用技术 ID 的列表。RCON 获取 JSON 输出。

        **参数：**

        - 无

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **语法：** `/getskinids`

        **描述：** 返回所有可用帕鲁皮肤 ID 的列表。RCON 获取 JSON 输出。

        **参数：**

        - 无

        **权限：** `Chat`、`RCON`、`Admin`

        **示例：**
        ```
        /getskinids
        ```
