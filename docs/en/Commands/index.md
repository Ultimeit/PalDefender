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
    ??? info "/reloadcfg"
        **Syntax:** `/reloadcfg`

        **Description:** Reloads `Config.json`, `whitelist.json` and `banlist.txt`.

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

    ??? warning "/iwantplayerlist"
        **Syntax:** `/iwantplayerlist`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /iwantplayerlist
        ```

    ??? warning "/togglepvp"
        **Syntax:** `/togglepvp`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /togglepvp
        ```

    ??? warning "/getpos"
        **Syntax:** `/getpos`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /getpos
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

    ??? warning "/send"
        **Syntax:** `/send`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /send
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

    ??? warning "/spectate"
        **Syntax:** `/spectate`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /spectate
        ```

??? note "Player Character"
    ??? info "/tp"
        **Syntax:** `/tp <UserId1> <UserId2>`

        **Description:** Teleports UserId1 to UserId2.

        **Arguments:**
        - `<UserId1>`: The player to teleport.
        - `<UserId2>`: The target player.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
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

    ??? warning "/givestats"
        **Syntax:** `/givestats`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /givestats
        ```

    ??? warning "/givemestats"
        **Syntax:** `/givemestats`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemestats
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

    ??? warning "/exportguilds"
        **Syntax:** `/exportguilds`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /exportguilds
        ```


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

    ??? warning "/give_relic"
        **Syntax:** `/give_relic`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /give_relic
        ```

    ??? warning "/giveme_relic"
        **Syntax:** `/giveme_relic`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /giveme_relic
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
        - `[Level]`: (Optional) Level of the Pal. Default: 1.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /givepal gdk_25300000000000000 Pal001 10
        ```

    ??? info "/givepal_j"
        **Syntax:** `/givepal_j <UserID> <PalTemplate>`

        **Description:** Gives a player a Pal defined by a PalTemplate file. Embedded JSON is no longer supported; only a filename is accepted.

        **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

        **Arguments:**
        - `<UserID>`: The ID of the player.
        - `<PalTemplate>`: The name of the PalTemplate file (see [PalTemplate](/FileTypes/PalTemplate)).

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
        - `[Level]`: (Optional) Level of the Pal. Default: 1.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemepal Pal001 10
        ```

    ??? info "/givemepal_j"
        **Syntax:** `/givemepal_j <PalTemplate>`

        **Description:** Gives yourself a Pal defined by a PalTemplate file. Embedded JSON is no longer supported; only a filename is accepted.

        **Arguments:**
        - `<PalTemplate>`: The name of the PalTemplate file (see [PalTemplate](/FileTypes/PalTemplate)).

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/summon"
        **Syntax:** `/summon <PalSummon>`

        **Description:** Spawns a Pal using the provided PalSummon file.

        **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

        **Arguments:**
        - `<PalSummon>`: The name of the PalSummon file to use.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /summon PalSummon
        ```

    ??? success "/giveegg"
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

            **Note:** Use the Pal's developer name, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level\]"
            **Description:** (Optional) The level of the Pal inside the egg.

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? success "/givemeegg"
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

            **Note:** Use the Pal's developer name, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level]"
            **Description:**  (Optional) The level of the Pal inside the egg.

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? warning "/giveegg_j"
        **Syntax:** `/giveegg_j`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /giveegg_j
        ```

    ??? warning "/givemeegg_j"
        **Syntax:** `/givemeegg_j`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemeegg_j
        ```

    ??? warning "/jetragon"
        **Syntax:** `/jetragon`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /jetragon
        ```

    ??? warning "/catwaifu"
        **Syntax:** `/catwaifu`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /catwaifu
        ```

    ??? warning "/exportpals"
        **Syntax:** `/exportpals`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /exportpals
        ```

    ??? warning "/deletepals"
        **Syntax:** `/deletepals`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /deletepals
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

    ??? warning "/givetechpoints"
        **Syntax:** `/givetechpoints`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /givetechpoints
        ```

    ??? warning "/givebosstechpoints"
        **Syntax:** `/givebosstechpoints`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /givebosstechpoints
        ```

    ??? warning "/givemetechpoints"
        **Syntax:** `/givemetechpoints`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemetechpoints
        ```

    ??? warning "/givemebosstechpoints"
        **Syntax:** `/givemebosstechpoints`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `Admin`

        **Example:**
        ```
        /givemebosstechpoints
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

    ??? warning "/getskinids"
        **Syntax:** `/getskinids`

        **Description:** (text still to be added)

        **Arguments:**
        - (text still to be added)

        **Permissions:** `Chat`, `RCON`, `Admin`

        **Example:**
        ```
        /getskinids
        ```