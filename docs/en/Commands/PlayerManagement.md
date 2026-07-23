# Player Management

## /kick { .toc-only }
??? info "/kick"
    **Syntax:** `/kick <UserId> [Reason="Kicked by Admin."]`

    **Description:** Kicks a player from the server.

    **Arguments:**

    - `<UserId>`: The ID of the player to kick.
    - `[Reason]`: (Optional) Reason for kicking. Default: "Kicked by Admin."

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /kick steam_76500000000000000 "Spamming in chat"
    ```

## /ban { .toc-only }
??? info "/ban"
    **Syntax:** `/ban <UserId> [Reason="Banned by Admin."]`

    **Description:** Bans and kicks a player from the server.

    **Arguments:**

    - `<UserId>`: The ID of the player to ban.
    - `[Reason]`: (Optional) Reason for banning. Default: "Banned by Admin."

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /ban gdk_25300000000000000 "Cheating"
    ```

## /ipban { .toc-only }
??? info "/ipban"
    **Syntax:** `/ipban <UserId> [Reason="Banned by Admin."]`

    **Description:** Bans a player's IP address and then kicks them from the server.

    **Arguments:**

    - `<UserId>`: The ID of the player to IP ban.
    - `[Reason]`: (Optional) Reason for banning. Default: "Banned by Admin."

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /ipban steam_76500000000000000
    ```

## /banip { .toc-only }
??? info "/banip"
    **Syntax:** `/banip <IP>`

    **Description:** Bans an IP address from the server.

    **Arguments:**

    - `<IP>`: The IP address to ban.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /banip 192.168.1.1
    ```

## /unbanip { .toc-only }
??? info "/unbanip"
    **Syntax:** `/unbanip <IP>`

    **Description:** Removes an IP address from the banlist.

    **Arguments:**

    - `<IP>`: The IP address to unban.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /unbanip 192.168.1.1
    ```

## /unban { .toc-only }
??? info "/unban"
    **Syntax:** `/unban <UserId> [Reason="Unbanned by admin."]`

    **Description:** Removes a UserId from the PalDefender ban list.

    **Arguments:**

    - `<UserId>`: The UserId to unban.
    - `[Reason]`: (Optional) Reason stored for the unban action.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /unban steam_76500000000000000 "Appeal accepted"
    ```

## /getip { .toc-only }
??? info "/getip"
    **Syntax:** `/getip <UserId>`

    **Description:** Shows you the IP address of a player.

    **Arguments:**

    - `<UserId>`: The ID of the player.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /getip gdk_25300000000000000
    ```

## /whitelist_add { .toc-only }
??? info "/whitelist_add"
    **Syntax:** `/whitelist_add <UserId>`

    **Description:** Adds a UserId to the whitelist.

    **Arguments:**

    - `<UserId>`: The ID of the player to whitelist.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /whitelist_add steam_76500000000000000
    ```

## /whitelist_remove { .toc-only }
??? info "/whitelist_remove"
    **Syntax:** `/whitelist_remove <UserId>`

    **Description:** Removes a UserId from the whitelist.

    **Arguments:**

    - `<UserId>`: The ID of the player to remove from whitelist.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /whitelist_remove gdk_25300000000000000
    ```

## /whitelist_get { .toc-only }
??? info "/whitelist_get"
    **Syntax:** `/whitelist_get`

    **Description:** Shows the full list of the whitelisted players.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /whitelist_get
    ```

## /imcheater { .toc-only }
??? info "/imcheater"
    **Syntax:** `/imcheater`

    **Description:** Use this to test how your server responds to a cheater.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /imcheater
    ```

## /spectate { .toc-only }
??? info "/spectate"
    **Syntax:** `/spectate`

    **Description:** Turns spectate mode on. Same as pressing hotkey `\`, but hotkey does not work for everyone, like console players.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /spectate
    ```






