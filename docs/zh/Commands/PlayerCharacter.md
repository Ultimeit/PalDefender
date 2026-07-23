# Player Character

## /tp { .toc-only }
??? info "/tp"
    **语法:**
    Any of the following works:

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

    **Note:** RCON must include the player being teleported because RCON has no in-game character.

    **参数:**

    - `<UserId>`: A player to teleport to, or the player being teleported when more arguments are supplied.
    - `<UserId1>`: 要传送的玩家。
    - `<UserId2>`: 目标玩家。
    - `<X> <Y> [Z]`: 地图坐标。如果省略 `Z`，PalDefender 会尝试寻找可用的地面高度。
    - `home`: Teleports to the nearest owned base.
    - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60`: Teleports to an oilrig destination.

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /tp steam_76500000000000000 gdk_25300000000000000
    /tp 100 -250
    /tp oilrig:Lv60
    ```

## /give_exp { .toc-only }
??? info "/give_exp"
    **语法:** `/give_exp <UserId> <Amount>`

    **描述:** 给玩家经验值。

    **参数:**

    - `<UserId>`: 玩家的 ID。
    - `<Amount>`: Amount of experience points.

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /give_exp gdk_25300000000000000 1000
    ```

## /giveme_exp { .toc-only }
??? info "/giveme_exp"
    **语法:** `/giveme_exp <Amount>`

    **描述:** 给自己经验值。

    **参数:**

    - `<Amount>`: Amount of experience points.

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /giveme_exp 1000
    ```

## /renameplayer { .toc-only }
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

## /givestats { .toc-only }
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

## /givemestats { .toc-only }
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

## /godmode { .toc-only }
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






