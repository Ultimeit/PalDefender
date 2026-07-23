# Research Tree

## /learntech { .toc-only }
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

## /unlearntech { .toc-only }
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

## /givetechpoints { .toc-only }
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

## /givebosstechpoints { .toc-only }
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

## /givemetechpoints { .toc-only }
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

## /givemebosstechpoints { .toc-only }
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







