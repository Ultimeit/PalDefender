# Pals

## /givepal { .toc-only }
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

## /givepal_j { .toc-only }
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

## /givemepal { .toc-only }
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

## /givemepal_j { .toc-only }
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

## /spawnpal { .toc-only }
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

## /spawnpal_j { .toc-only }
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

## /summon { .toc-only }
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

## /giveegg { .toc-only }
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


## /givemeegg { .toc-only }
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
        **Description:** The Pal that will be inside the egg.

        **Note:** Use the Pal ID, e.g., `WeaselDragon` (Chillet). See the full list at [paldeck.cc/pals](https://paldeck.cc/pals).

    ??? quote "[Level]"
        **Description:** (Optional) The level of the Pal inside the egg.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /givemeegg PalEgg_Ice_01 WeaselDragon 10
    ```

## /giveegg_j { .toc-only }
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

## /givemeegg_j { .toc-only }
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

## /jetragon { .toc-only }
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

## /catwaifu { .toc-only }
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

## /exportpals { .toc-only }
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

## /deletepals { .toc-only }
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

        For more details, see the [PalFilter documentation](https://github.com/Ultimeit/PalDefender/blob/master/Wiki/Commands/deletepals.md).

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
    /deletepals 76567890987654321 ID Anubis Rank>=3
    /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
    ```







