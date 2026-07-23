# Server Management

## /version { .toc-only }
??? info "/version"
    **Syntax:** `/version`

    **Description:** Shows the Palworld game version and PalDefender version. RCON returns JSON output.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /version
    ```

## /reloadcfg { .toc-only }
??? info "/reloadcfg"
    **Syntax:** `/reloadcfg`

    **Description:** Reloads `Config.json`, `WhiteList.json`, and PalDefender ban data.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /reloadcfg
    ```

## /addadminip { .toc-only }
??? info "/addadminip"
    **Syntax:** `/addadminip <IP>`

    **Description:** Adds an IP address to admin whitelist.

    **Arguments:**

    - `<IP>`: The IP address to add as admin.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /addadminip 192.168.1.1
    ```

## /setadmin { .toc-only }
??? info "/setadmin"
    **Syntax:** `/setadmin <UserId>`

    **Description:** Temporarily grants/revokes admin from a player.

    **Arguments:**

    - `<UserId>`: The ID of the player to grant/revoke admin.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /setadmin steam_76500000000000000
    ```

## /pgbroadcast { .toc-only }
??? info "/pgbroadcast"
    **Syntax:** `/pgbroadcast <Message>`

    **Description:** Send a message to all players in the server.

    **Arguments:**

    - `<Message>`: The message to broadcast.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /pgbroadcast "Server will restart soon."
    ```

## /adminlogin { .toc-only }
??? info "/adminlogin"
    **Syntax:** `/adminlogin <password>`

    **Description:** Logs you into admin mode. Requires your admin password as an argument.

    **Arguments:**

    - `<password>`: The admin password.

    **Permissions:** `Chat`

    **Example:**
    ```
    /adminlogin mySecretPassword
    ```

## /adminlogout { .toc-only }
??? info "/adminlogout"
    **Syntax:** `/adminlogout`

    **Description:** Logs you out of admin mode.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /adminlogout
    ```

## /iwantplayerlist { .toc-only }
??? info "/iwantplayerlist"
    **Syntax:** `/iwantplayerlist`

    **Description:** Enables the in-game player list overlay, allowing you to view every player's UserId and Player UID when you press ESC. Useful for server admins and players who want to see detailed player information directly in the game interface.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /iwantplayerlist
    ```

## /getpos { .toc-only }
??? info "/getpos"
    **Syntax:** `/getpos [\[UserId\]]{ .var-command-optional }`

    **Description:** Gets your current position in the world, which can be used for teleporting, summoning, and similar actions. If a [UserId] is provided, gets the position of that player instead.

    **Arguments:**

    - `[UserId]`: (Optional) The ID of the player whose position you want to get. If omitted, gets your own position.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /getpos
    /getpos steam_76500000000000000
    ```

## /settime { .toc-only }
??? info "/settime"
    **Syntax:** `/settime <hour>`

    **Description:** Changes the time in Palworld. Hour can have following values: `0` to `23`, `day` and `night`.

    **Arguments:**

    - `<hour>`: Hour value (0-23, day, night).

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /settime 12
    /settime night
    ```

## /togglepvp { .toc-only }
??? info "/togglepvp"
    **Syntax:** `/togglepvp`

    **Description:** Toggles server PvP on or off for the current running session.

    **Arguments:**

    - None

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /togglepvp
    ```

## /alert { .toc-only }
??? info "/alert"
    **Syntax:** `/alert <message>`

    **Description:** Sends an alert message to all players on the server. This message is usually displayed prominently on their screens.

    **Arguments:**

    - `<message>`: The message to broadcast as an alert.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /alert Server will restart in 5 minutes!
    ```

## /send { .toc-only }
??? info "/send"
    **Syntax:** `/send <type> <UserId> <Message>`

    **Description:** Allows you to send a message or log message to a specific player.

    **Arguments:**

    - `<type>`: The type of message to send. Possible values:
         - `msg`: Regular chat message.
         - `log`: Regular log message (white, disappears quickly, larger font).
         - `ilog`: Important log message (blue, stays longer).
         - `vilog`: Very important log message (blue, stays extremely long).
    - `<UserId>`: The ID of the player to receive the message.
    - `<Message>`: The message text to send.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /send msg steam_76500000000000000 Dont miss out on Qonzer's sale!
    /send log steam_76500000000000000 Dont miss out on Qonzer's sale!
    /send ilog steam_76500000000000000 Dont miss out on Qonzer's sale!
    /send vilog steam_76500000000000000 Dont miss out on Qonzer's sale!
    ```







