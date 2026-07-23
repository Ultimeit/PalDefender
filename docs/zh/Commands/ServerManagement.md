# Server Management

## /version { .toc-only }
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

## /reloadcfg { .toc-only }
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

## /addadminip { .toc-only }
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

## /setadmin { .toc-only }
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

## /pgbroadcast { .toc-only }
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

## /adminlogin { .toc-only }
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

## /adminlogout { .toc-only }
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

## /iwantplayerlist { .toc-only }
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

## /getpos { .toc-only }
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

## /settime { .toc-only }
??? info "/settime"
    **语法:** `/settime <hour>`

    **描述:** 更改 Palworld 中的时间。小时可为 `0` 到 `23`，也可以是 `day` 或 `night`。

    **参数:**

    - `<hour>`: Hour value (0-23, day, night).

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /settime 12
    /settime night
    ```

## /togglepvp { .toc-only }
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

## /alert { .toc-only }
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

## /send { .toc-only }
??? info "/send"
    **语法:** `/send <type> <UserId> <Message>`

    **描述:** 允许你向指定玩家发送消息或日志消息。

    **参数:**

    - `<type>`: 要发送的消息类型。可选值：
         - `msg`: Regular chat message.
         - `log`: Regular log message (white, disappears quickly, larger font).
         - `ilog`: Important log message (blue, stays longer).
         - `vilog`: Very important log message (blue, stays extremely long).
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






