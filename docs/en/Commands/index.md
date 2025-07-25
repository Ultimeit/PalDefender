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


??? note "Server Management Commands"
    | Command | Description | Permissions |
    | ------- | ----------- | ----------- |
    | `/kick <UserId> [Reason="Kicked by Admin."]` | Kicks a player from the server. | `Chat` `RCON` `Admin` |
    | `/ban <UserId> [Reason="Banned by Admin."]` | Bans and kicks a player from the server. | `Chat` `RCON` `Admin` |
    | `/ipban <UserId> [Reason="Banned by Admin."]` | Bans a player IP address and then and kicks them from the server. | `Chat` `RCON` `Admin` |
    | `/banip <IP>` | Bans an IP address from the server. | `Chat` `RCON` `Admin` |
    | `/unbanip <IP>` | Removes an IP address from the banlist. | `Chat` `RCON` `Admin` |
    | `/getip <UserId>` | Shows you the IP address of a player. | `Chat` `RCON` `Admin` |
    | `/whitelist_add <UserId>` | Adds a UserId to the whitelist. | `Chat` `RCON` `Admin` |
    | `/whitelist_remove <UserId>` | Removes a UserId from the whitelist. | `Chat` `RCON` `Admin` |
    | `/whitelist_get` | Shows the full list of the whitelisted players. | `Chat` `RCON` `Admin` |
    | `/addadminip <IP>` | Adds a IP address to admin whitelist. | `Chat` `RCON` `Admin` |
    | `/setadmin <UserId>` | Temporarily grants/revokes admin from a player. | `Chat` `RCON` `Admin` |
    | `/adminlogout` | Logs you out of admin mode. | `Chat` `Admin` |
    | `/adminlogin` | Logs you into admin mode. | `Chat` |
    | `/setguildleader <UserId>` | Makes target player the leader of his current guild. | `Chat` `RCON` `Admin` |
    | `/renameplayer <UserId> <NewName>` | Renames a player's nickname. | `Chat` `RCON` `Admin` |
    | `/pgbroadcast <Message>` | Send a message to all players in the server. | `Chat` `RCON` `Admin` |
    | `/reloadcfg` | Reloads `Config.json`, `whitelist.json` and `banlist.txt`. | `Chat` `RCON` `Admin` |
    | `/getrconcmds` | Returns a list of every command with the required arg count which is usable by RCON. | `RCON` `Admin` |


??? note "Admin Exclusive Commands"
    | Command | Description | Permissions |
    | ------- | ----------- | ----------- |
    | `/imcheater` | Use this to test how your server response to a cheater. | `Chat` `Admin` |
    | `/godmode [on/off]` | Makes you invulnerable and allows one shotting anything. | `Chat` `Admin` |
    | `/jetragon` | Gives you a extremely fast Jetragon named `PalGuardian`. | `Chat` `Admin` |
    | `/catwaifu` | Gives you an Cat-Waifu (Katress) that buffs your character stats. | `Chat` `Admin` |

??? note "World Commands"
    | Command | Description | Permissions |
    | ------- | ----------- | ----------- |
    | `/goto <X> <Y> [Z]` | Teleports you to the location. | `Chat` `Admin` |
    | `/gotonearestbase [X] [Y] [Z]` | Teleports you to the nearest base of the location. | `Chat` `Admin` |
    | `/getnearestbase [X] [Y] [Z]` | Tells you guild name which owns base nearest to your character. | `Chat` `RCON` `Admin` |
    | `/killnearestbase [X] [Y] [Z]` | Destroys nearest base (**Use with caution!**). | `Chat` `RCON` `Admin` |
    | `/settime <hour>` | Changes the time in Palworld. Hour can have following values: `0` to `23`, `day` and `night`. | `Chat` `RCON` `Admin` |
    | `/resetoilrig <oilrig>` | Resets the specified OilRigs. Only the rocket tower is unaffected. Argument can have following values: `lv30`, `lv55`, `lv60` and `all`. | `Chat` `RCON` `Admin` |
    | `/tp <UserId1> <UserId2>` | Teleports UserId1 to UserId2. | `Chat` `RCON` `Admin` |
    | `/tp <UserId> <X> <Y> <Z>` | Teleports the player to coordinates. | `Chat` `RCON` `Admin` |
    | `/tp <UserId> home` | Teleports the player to their closest base. | `Chat` `RCON` `Admin` |
    | `/tp <UserId> oilrig` | Teleports the player to their closest oilrig. | `Chat` `RCON` `Admin` |
    | `/tp <UserId>` | Teleports you to the player. | `Chat` `RCON` `Admin` |

??? note "Item Commands"
    | Command | Description | Permissions |
    | ------- | ----------- | ----------- |
    | `/give <UserId> <ItemId> [Amount=1]` | Gives a player an item and if specified how many. | `Chat` `RCON` `Admin` |
    | `/giveitems <UserId> <ItemId>[:<Amount>] ...` | Gives a player more than 1 item in one command and if specified how many of each seperated by a colon. | `Chat` `RCON` `Admin` |
    | `/giveme <ItemId> [Amount=1]` | Gives yourself an item and if specified how many. | `Chat` `Admin` |
    | `/delitem <UserId> <ItemId> [Amount=1]` | Deletes an item from a player and if specified how many. Default is `1` which will delete only 1 occurence of that item. Use `all` instead of `1` to delete all occurences. | `Chat` `RCON` `Admin` |
    | `/delitems <UserId> <ItemId>[:<Amount>] ...` | Deletes more than 1 item from a player in one command and if specified how many of each seperated by a colon. Use `all` instead of `1` to delete all occurences. | `Chat` `RCON` `Admin` |
    | `/givepal <UserId> <PalId> [Level=1]` | Gives a Pal to a player at the specified level. | `Chat` `RCON` `Admin` |
    | `/givepal_j <UserID> <PalJSON>` | Gives player a Pal defined by a JSON blob. | `Chat` `RCON` `Admin` |
    | `/givemepal <PalId> [Level=1]` | Gives yourself a Pal at the specified level. | `Chat` `Admin` |
    | `/givemepal_j <PalJSON>` | Gives yourself a Pal defined by a JSON blob. | `Chat` `Admin` |
    | `/give_exp <UserId> <Amount>` | Gives experience points to a player. | `Chat` `RCON` `Admin` |
    | `/giveme_exp <Amount>` | Gives experience points to yourself. | `Chat` `Admin` |
    | `/summon <PalSummon.json>` | Spawns a Pal using the provided `PalSummon.json` file. | `Chat` `Admin` |
    | `/clearinv <UserId> [Container=items] ...` | Clears specified containers from a player's inventory. Available containers: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot`, or `all`. | `Chat` `RCON` `Admin` |

??? note "Technology Commands"
    | Command | Description | Permissions |
    | ------- | ----------- | ----------- |
    | `/learntech <UserId> <TechID>` | Lets a player learn a specific technology. Use `all` to unlock everything. | `Chat` `RCON` `Admin` |
    | `/unlearntech <UserId> <TechID>` | Makes a player forget a specific technology. Use `all` to remove everything. | `Chat` `RCON` `Admin` |
    | `/gettechids` | Returns a list of all available technology IDs. RCON gets JSON output. | `Chat` `RCON` `Admin` |