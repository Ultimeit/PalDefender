# Player Character

## /tp { .toc-only }
??? info "/tp"
    **Syntax:**
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

    **Description:** Teleports yourself, or a specified player, to another player, coordinates, the nearest owned base, or an oilrig destination.

    **Note:** RCON must include the player being teleported because RCON has no in-game character.

    **Arguments:**

    - `<UserId>`: A player to teleport to, or the player being teleported when more arguments are supplied.
    - `<UserId1>`: The player to teleport.
    - `<UserId2>`: The target player.
    - `<X> <Y> [Z]`: Map coordinates. If `Z` is omitted, PalDefender tries to find a usable ground height.
    - `home`: Teleports to the nearest owned base.
    - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60`: Teleports to an oilrig destination.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /tp steam_76500000000000000 gdk_25300000000000000
    /tp 100 -250
    /tp oilrig:Lv60
    ```

## /give_exp { .toc-only }
??? info "/give_exp"
    **Syntax:** `/give_exp <UserId> <Amount>`

    **Description:** Gives experience points to a player.

    **Arguments:**

    - `<UserId>`: The ID of the player.
    - `<Amount>`: Amount of experience points.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /give_exp gdk_25300000000000000 1000
    ```

## /giveme_exp { .toc-only }
??? info "/giveme_exp"
    **Syntax:** `/giveme_exp <Amount>`

    **Description:** Gives experience points to yourself.

    **Arguments:**

    - `<Amount>`: Amount of experience points.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /giveme_exp 1000
    ```

## /renameplayer { .toc-only }
??? info "/renameplayer"
    **Syntax:** `/renameplayer <UserId> <NewName>`

    **Description:** Renames a player's nickname.

    **Arguments:**

    - `<UserId>`: The ID of the player.
    - `<NewName>`: The new nickname.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /renameplayer steam_76500000000000000 NewNickname
    ```

## /givestats { .toc-only }
??? info "/givestats"
    **Syntax:** `/givestats <UserId> [Count=1]`

    **Description:** Gives the player one or more Unused Status Points (negative value will subtract). Does not affect points that are already spent.

    **Arguments:**

    - `<UserId>`: The ID of the player to receive the status points.
    - `[Count]`: (Optional) The number of Unused Status Points to give (can be negative to subtract). Default: 1.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /givestats steam_76500000000000000 5
    /givestats steam_76500000000000000 -2
    ```

## /givemestats { .toc-only }
??? info "/givemestats"
    **Syntax:** `/givemestats [Count=1]`

    **Description:** Gives yourself one or more Unused Status Points (negative value will subtract). Does not affect points that are already spent.

    **Arguments:**

    - `[Count]`: (Optional) The number of Unused Status Points to give yourself (can be negative to subtract). Default: 1.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /givemestats 5
    /givemestats -2
    ```

## /godmode { .toc-only }
??? info "/godmode"
    **Syntax:** `/godmode [on/off]`

    **Description:** Grants invulnerability including status effect immunity, denies consumption of food and restores health upon activation. Optionally allows one-shotting everything, if enabled in the config.

    **Arguments:**

    - `[on/off]`: (Optional) To explicitly enable or disable the godmode. Default: Toggles on and off.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /godmode
    /godmode on
    /godmode off
    ```






