# Research Tree

## /learntech { .toc-only }
??? info "/learntech"
    **Syntax:** `/learntech <UserId> <TechID>`

    **Description:** Lets a player learn a specific technology. Use `all` to unlock everything.

    **Arguments:**

    - `<UserId>`: The ID of the player.
    - `<TechID>`: The technology to learn. Use `all` to unlock everything.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /learntech steam_76500000000000000 Tech001
    /learntech gdk_25300000000000000 all
    ```

## /unlearntech { .toc-only }
??? info "/unlearntech"
    **Syntax:** `/unlearntech <UserId> <TechID>`

    **Description:** Makes a player forget a specific technology. Use `all` to remove everything.

    **Arguments:**

    - `<UserId>`: The ID of the player.
    - `<TechID>`: The technology to forget. Use `all` to remove everything.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /unlearntech gdk_25300000000000000 Tech001
    /unlearntech steam_76500000000000000 all
    ```

## /givetechpoints { .toc-only }
??? info "/givetechpoints"
    **Syntax:** `/givetechpoints <UserId> [Amount=1]`

    **Description:** Gives the target user X technology points.

    **Arguments:**

    - `<UserId>`: The ID of the player to receive the technology points.
    - `[Amount]`: (Optional) The number of technology points to give. Default: 1.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /givetechpoints steam_76500000000000000 10
    ```

## /givebosstechpoints { .toc-only }
??? info "/givebosstechpoints"
    **Syntax:** `/givebosstechpoints <UserId> [Amount=1]`

    **Description:** Gives the target user X ancient technology points.

    **Arguments:**

    - `<UserId>`: The ID of the player to receive the ancient technology points.
    - `[Amount]`: (Optional) The number of ancient technology points to give. Default: 1.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /givebosstechpoints steam_76500000000000000 5
    ```

## /givemetechpoints { .toc-only }
??? info "/givemetechpoints"
    **Syntax:** `/givemetechpoints [Amount=1]`

    **Description:** Gives yourself X technology points.

    **Arguments:**

    - `[Amount]`: (Optional) The number of technology points to give yourself. Default: 1.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /givemetechpoints 10
    ```

## /givemebosstechpoints { .toc-only }
??? info "/givemebosstechpoints"
    **Syntax:** `/givemebosstechpoints [Amount=1]`

    **Description:** Gives yourself X ancient technology points.

    **Arguments:**

    - `[Amount]`: (Optional) The number of ancient technology points to give yourself. Default: 1.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /givemebosstechpoints 5
    ```







