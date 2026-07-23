# Player Management

## /kick { .toc-only }
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

## /ban { .toc-only }
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

## /ipban { .toc-only }
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

## /banip { .toc-only }
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

## /unbanip { .toc-only }
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

## /unban { .toc-only }
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

## /getip { .toc-only }
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

## /whitelist_add { .toc-only }
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

## /whitelist_remove { .toc-only }
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

## /whitelist_get { .toc-only }
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

## /imcheater { .toc-only }
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

## /spectate { .toc-only }
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






