# Commands

## What Are Commands?

Commands are special text-based instructions that allow you to interact with the game. By typing commands into the chat, you can perform actions like teleporting, spawning creatures, or managing players. Commands usually start with a <span class="var-command">/</span> followed by the command name and optional arguments.

## Who Can Use Commands?

**Currently there is no command that non-admin player can use.**
At the current version there are only Admin and RCON commands available.

## Commands List

!!! note "Command Syntax"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → Must be included.<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → Can be omitted. The <span class="var-command-optional">{?}</span> indicates the default value being used when omitted.
    </p>
    <p>
    Arguments have different types. The most common are <span class="var-string">strings</span>, <span class="var-number">numbers</span>, <span class="var-float">floats</span> and <span class="var-bool">booleans</span>. Some command even have complex types such as specific <span class="file">filenames</span> in a special directory or actually a <span class="var-filter">filter</span>.
    </p>

!!! tip "<span class='pd-badge pd-badge--beta'>Beta</span> ID lookup"
    Use [paldeck.cc/pals](https://paldeck.cc/pals) for `PalID`, [paldeck.cc/items](https://paldeck.cc/items) for `ItemID`, [paldeck.cc/technology](https://paldeck.cc/technology) for `TechID`, [paldeck.cc/buildings](https://paldeck.cc/buildings) for `BuildingID`, [paldeck.cc/passives](https://paldeck.cc/passives) for `PassiveID`, and [paldeck.cc/skills](https://paldeck.cc/skills) for skill IDs.

??? note "RCON only"
    ??? info "/getrconcmds"
        **Syntax:** `/getrconcmds`

        **Description:** Returns a list of every command with the required arg count which is usable by RCON.

        **Arguments:**

        - None

        **Permissions:** `RCON`

        **Example:**
        ```
        /getrconcmds
        ```

??? note "Server Management"
    ??? info "/version"
        **Syntax:** `/version`

        **Description:** <span class='pd-badge pd-badge--beta'>Beta</span> Shows the Palworld game version and PalDefender version. RCON returns JSON output.

        **Arguments:**

        - None

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /version
        ```

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

    ??? info "/getpos"
        **Syntax:** `/getpos [UserId]`

        **Description:** Gets your current position in the world, which can be used for teleporting, summoning, and similar actions. If a [UserId] is provided, gets the position of that player instead.

        **Arguments:**

        - `[UserId]`: (Optional) The ID of the player whose position you want to get. If omitted, gets your own position.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

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

    ??? info "/togglepvp"
        **Syntax:** `/togglepvp`

        **Description:** <span class='pd-badge pd-badge--beta'>Beta</span> Toggles server PvP on or off for the current running session.

        **Arguments:**

        - None

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /togglepvp
        ```

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

??? note "Base Management"
    ??? info "/getnearestbase"
        **Syntax:** `/getnearestbase [X] [Y] [Z]`

        **Description:** Tells you the guild name which owns the base nearest to your character.

        **Note:** When executed via **RCON**, all location parameters (`[X]` `[Y]` `[Z]`) **are required**, since RCON has no player character to determine the location.

        **Arguments:**

        - `[X]`: (Optional) X coordinate.
        - `[Y]`: (Optional) Y coordinate.
        - `[Z]`: (Optional) Z coordinate.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **Syntax:** `/gotonearestbase [X] [Y] [Z]`

        **Description:** Teleports you to the nearest base of the location.

        **Note:** When executed via **RCON**, all location parameters (`[X]` `[Y]` `[Z]`) **are required**, since RCON has no player character to determine the location.

        **Arguments:**

        - `[X]`: (Optional) X coordinate.
        - `[Y]`: (Optional) Y coordinate.
        - `[Z]`: (Optional) Z coordinate.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **Syntax:** `/killnearestbase [X] [Y] [Z]`

        **Description:** Destroys the nearest base (**Use with caution!**).

        **Note:** When executed via **RCON**, all location parameters (`[X]` `[Y]` `[Z]`) **are required**, since RCON has no player character to determine the location.

        **Arguments:**

        - `[X]`: (Optional) X coordinate.
        - `[Y]`: (Optional) Y coordinate.
        - `[Z]`: (Optional) Z coordinate.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "Player Management"
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

    ??? info "/unban"
        **Syntax:** `/unban <UserId> [Reason="Unbanned by admin."]`

        **Description:** <span class='pd-badge pd-badge--beta'>Beta</span> Removes a UserId from the PalDefender ban list.

        **Arguments:**

        - `<UserId>`: The UserId to unban.
        - `[Reason]`: (Optional) Reason stored for the unban action.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /unban steam_76500000000000000 "Appeal accepted"
        ```

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

??? note "Player Character"
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

        **Note:** <span class='pd-badge pd-badge--beta'>Beta</span> RCON must include the player being teleported because RCON has no in-game character.

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

??? note "Guild Management"
    ??? info "/setguildleader"
        **Syntax:** `/setguildleader <UserId>`

        **Description:** Makes target player the leader of his current guild.

        **Arguments:**

        - `<UserId>`: The ID of the player to make guild leader.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **Syntax:** `/exportguilds`

        **Description:** Dumps every guild of the server into Pal/Binaries/Win64/PalDefender/guildexport.json.

        **Arguments:**

        - None

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /exportguilds
        ```
        Example output file: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "Items"
    ??? info "/give"
        **Syntax:** `/give <UserId> <ItemId> [Amount=1]`

        **Description:** Gives a player an item and if specified how many.

        **Arguments:**

        - `<UserId>`: The ID of the player to give the item to.
        - `<ItemId>`: The item to give.
        - `[Amount]`: (Optional) How many. Default: 1.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **Syntax:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **Description:** Gives a player more than 1 item in one command and if specified how many of each separated by a colon.

        **Arguments:**

        - `<UserId>`: The ID of the player to give the items to.
        - `<ItemId>[:<Amount>] ...`: List of items and optional amounts.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **Syntax:** `/giveme <ItemId> [Amount=1]`

        **Description:** Gives yourself an item and if specified how many.

        **Arguments:**

        - `<ItemId>`: The item to give yourself.
        - `[Amount]`: (Optional) How many. Default: 1.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **Syntax:** `/delitem <UserId> <ItemId> [Amount=1]`

        **Description:** Deletes an item from a player and if specified how many. Default is `1` which will delete only 1 occurrence of that item. Use `all` instead of `1` to delete all occurrences.

        **Arguments:**

        - `<UserId>`: The ID of the player.
        - `<ItemId>`: The item to delete.
        - `[Amount]`: (Optional) How many. Default: 1. Use `all` to delete all occurrences.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **Syntax:** `/give_relic <UserId> <Amount>`

        **Description:** Gives the player one or more Lifmunk Effigies.

        **Arguments:**

        - `<UserId>`: The ID of the player to receive the Lifmunk Effigies.
        - `<Amount>`: The number of Lifmunk Effigies to give.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /give_relic steam_76500000000000000 5
        ```

    ??? info "/giveme_relic"
        **Syntax:** `/giveme_relic <Amount>`

        **Description:** Gives yourself one or more Lifmunk Effigies.

        **Arguments:**

        - `<Amount>`: The number of Lifmunk Effigies to give yourself.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /giveme_relic 5
        ```


    ??? info "/delitems"
        **Syntax:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **Description:** Deletes more than 1 item from a player in one command and if specified how many of each separated by a colon. Use `all` instead of `1` to delete all occurrences.

        **Arguments:**

        - `<UserId>`: The ID of the player.
        - `<ItemId>[:<Amount>] ...`: List of items and optional amounts.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **Syntax:** `/clearinv <UserId> [Container=items] ...`

        **Description:** Clears specified containers from a player's inventory. Available containers: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot`, or `all`.

        **Arguments:**

        - `<UserId>`: The ID of the player.
        - `[Container] ...`: (Optional) Containers to clear. Default: items.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "Pals"
    ??? info "/givepal"
        **Syntax:** `/givepal <UserId> <PalId> [Level=1]`

        **Description:** Gives a Pal to a player at the specified level.

        **Arguments:**

        - `<UserId>`: The ID of the player.
        - `<PalId>`: The Pal to give.
            - **Note:** Use the Pal ID, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Optional) Level of the Pal. Default: 1.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **Syntax:** `/givepal_j <UserID> <PalTemplate>`

        **Description:** Gives a player a Pal defined by a PalTemplate file. Embedded JSON is no longer supported; only a filename is accepted.

        **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

        **Arguments:**

        - `<UserID>`: The ID of the player.
        - `<PalTemplate>`: The name of the PalTemplate file (see [PalTemplate](../FileTypes/PalTemplate.md)).

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **Syntax:** `/givemepal <PalId> [Level=1]`

        **Description:** Gives yourself a Pal at the specified level.

        **Arguments:**

        - `<PalId>`: The Pal to give yourself.
            - **Note:** Use the Pal ID, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Optional) Level of the Pal. Default: 1.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **Syntax:** `/givemepal_j <PalTemplate>`

        **Description:** Gives yourself a Pal defined by a PalTemplate file. Embedded JSON is no longer supported; only a filename is accepted.

        **Arguments:**

        - `<PalTemplate>`: The name of the PalTemplate file (see [PalTemplate](../FileTypes/PalTemplate.md)).

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **Syntax:**
        Any of the following works:

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **Description:** Spawns a Pal relative or absolute to you. **RCON has to specify x, y and z!**

        **Note:** All stats, except level, are randomized.

        **Arguments:**
        - `<PalID>`: The Pal to spawn.
        - `[x]`: (Optional) x position of the pal. Default: Relative to player-invoker.
        - `[y]`: (Optional) y position of the pal. Default: Relative to player-invoker.
        - `[z]`: (Optional) z position of the pal. Default: Relative to player-invoker.
        - `[Level]`: (Optional) Level of the Pal. Default: 1.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /spawnpal Anubis 255
        ```
        _Spawns an Anubis with level 255!_

    ??? info "/spawnpal_j"
        **Syntax:**

        Any of the following works:

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal <PalTemplate> [x] [y] [z]`

        **Description:** Spawns a Pal relative or absolute to you. **RCON has to specify x, y and z!**

        **Note:** All stats, except level, are randomized.

        **Arguments:**

        - `<PalTemplate>`: The name of the PalTemplate file to use.
        - `[x]`: (Optional) x position of the pal. Default: Relative to player-invoker.
        - `[y]`: (Optional) y position of the pal. Default: Relative to player-invoker.
        - `[z]`: (Optional) z position of the pal. Default: Relative to player-invoker.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /spawnpal Anubis 255
        ```
        _Spawns an Anubis with level 255!_

    ??? info "/summon"
        **Syntax:** `/summon <PalSummon>`

        **Description:** Spawns a Pal using the provided PalSummon file.

        **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

        **Arguments:**
        - `<PalSummon>`: The name of the PalSummon file to use.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **Syntax:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **Description:** Gives target user a pal egg with the specific pal inside and optionally adjusted level.

        **Arguments:**

        ??? quote "<UserId\>"
            **Description:** The ID of the player to receive the egg.

        ??? quote "<EggId\>"
            **Description:** The type of egg to give.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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
            **Description:** The Pal that will be inside the egg.

            **Note:** Use the Pal ID, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level\]"
            **Description:** (Optional) The level of the Pal inside the egg.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **Syntax:** `/givemeegg <EggId> <PalId> [Level]`

        **Description:** Gives yourself a pal egg with the specific pal inside and optionally adjusted level.

        **Arguments:**

        ??? quote "<EggId\>"
            **Description:** The type of egg to give yourself.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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
            **Description:**  The Pal that will be inside the egg.

            **Note:** Use the Pal ID, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level]"
            **Description:**  (Optional) The level of the Pal inside the egg.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **Syntax:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **Description:** Gives a pal egg with a Pal defined by a PalTemplate file and optionally adjusted level.

        **Arguments:**

        ??? quote "<EggId\>"
            **Description:** The type of egg to give.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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
            **Description:** The name of the PalTemplate file to use.

            **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing. See [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Level]"
            **Description:** (Optional) The level of the Pal inside the egg.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **Syntax:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **Description:** Gives yourself a pal egg with a Pal defined by a PalTemplate file and optionally adjusted level.

        **Arguments:**

        ??? quote "<EggI\>"
            **Description:** The type of egg to give yourself.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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
            **Description:** The name of the PalTemplate file to use.

            **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing. See [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Level]"
            **Description:** (Optional) The level of the Pal inside the egg.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **Syntax:** `/jetragon`

        **Description:** Gives you an Admin-Jetragon Pal (it's faaas.... gone).

        **Arguments:**
        - None

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **Syntax:** `/catwaifu`

        **Description:** Gives you an Admin-Cat-Waifu that buffs your character stats.

        **Arguments:**

        - None

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **Syntax:** `/exportpals [UserId]`

        **Description:** Export every Pal of a player to a PalTemplate file at Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/.

        **Arguments:**

        - `[UserId]`: (Optional) The ID of the player whose Pals will be exported. If omitted, exports your own Pals.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **Syntax:** `/deletepals <UserId> <PalFilter>`

        **Description:** Deletes Pals from the specified user using advanced filters. The filter allows you to specify multiple criteria (such as Pal ID, level, gender, passives, etc.) in one command. Please test in a safe environment before using on important data.

        **Arguments:**

        ??? quote "<UserId\>"
            **Description:** The ID of the player whose Pals will be deleted.

        ??? quote "<PalFilter\>"
            **Description:** A set of filter keywords to select which Pals to delete.

            **Note:** Multiple keywords can be combined in one command.

            Available filter keywords:

            - `ID`: PalID or list of PalIDs (comma-separated)
            - `Nick`: String (name of the Pal)
            - `Gender`: `male` or `female`
            - `Level`: Number, supports symbols `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank`: Number, supports symbols `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky`: `true` or `false` (shiny)
            - `Passives`: PassiveSkill or list of PassiveSkills (comma-separated)
            - `Limit`: Number (max number of Pals to delete)

            **Example filters:**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            For more details, see the [PalFilter documentation](https://github.com/Ultimeit/PalDefender/blob/<span class='pd-badge pd-badge--beta'>Beta</span>/Wiki/Commands/deletepals.md).

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "Research Tree"
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


??? note "Data mining"
    ??? info "/gettechids"
        **Syntax:** `/gettechids`

        **Description:** Returns a list of all available technology IDs. RCON gets JSON output.

        **Arguments:**

        - None

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **Syntax:** `/getskinids`

        **Description:** Returns a list of all available Pal Skin IDs. RCON gets JSON output.

        **Arguments:**

        - None

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /getskinids
        ```
