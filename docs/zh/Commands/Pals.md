# Pals

## /givepal { .toc-only }
??? info "/givepal"
    **语法:** `/givepal <UserId> <PalId> [Level=1]`

    **描述:** 给玩家一只指定等级的帕鲁。

    **参数:**

    - `<UserId>`: 玩家的 ID。
    - `<PalId>`: 要给予的帕鲁。
        - **Note:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。
    - `[Level]`: （可选）Pal 等级。默认：1。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /givepal gdk_25300000000000000 WeaselDragon 10
    ```

## /givepal_j { .toc-only }
??? info "/givepal_j"
    **语法:** `/givepal_j <UserID> <PalTemplate>`

    **描述:** 给玩家一只由 PalTemplate 文件定义的帕鲁。不再支持内嵌 JSON，只接受文件名。

    **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

    **参数:**

    - `<UserID>`: 玩家的 ID。
    - `<PalTemplate>`: PalTemplate 文件名（见 [PalTemplate](../FileTypes/PalTemplate.md)）。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /givepal_j steam_76500000000000000 MyPalTemplate
    ```

## /givemepal { .toc-only }
??? info "/givemepal"
    **语法:** `/givemepal <PalId> [Level=1]`

    **描述:** 给自己一只指定等级的帕鲁。

    **参数:**

    - `<PalId>`: 要给自己的帕鲁。
        - **Note:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。
    - `[Level]`: （可选）Pal 等级。默认：1。

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /givemepal WeaselDragon 10
    ```

## /givemepal_j { .toc-only }
??? info "/givemepal_j"
    **语法:** `/givemepal_j <PalTemplate>`

    **描述:** 给自己一只由 PalTemplate 文件定义的帕鲁。不再支持内嵌 JSON，只接受文件名。

    **参数:**

    - `<PalTemplate>`: PalTemplate 文件名（见 [PalTemplate](../FileTypes/PalTemplate.md)）。

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /givemepal_j MyPalTemplate
    ```

## /spawnpal { .toc-only }
??? info "/spawnpal"
    **语法:**
    Any of the following works:

    - `/spawnpal <PalID>`
    - `/spawnpal <PalID> [Level]`
    - `/spawnpal <PalID> [x] [y] [z]`
    - `/spawnpal <PalID> [x] [y] [z] [Level]`

    **描述:** 按相对或绝对坐标生成一只帕鲁。**RCON 必须指定 x、y 和 z！**

    **Note:** All stats, except level, are randomized.

    **参数:**
    - `<PalID>`: 要生成的帕鲁。
    - `[x]`: （可选）Pal 的 X 坐标。默认：相对于执行命令的玩家。
    - `[y]`: （可选）Pal 的 Y 坐标。默认：相对于执行命令的玩家。
    - `[z]`: （可选）Pal 的 Z 坐标。默认：相对于执行命令的玩家。
    - `[Level]`: （可选）Pal 等级。默认：1。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /spawnpal Anubis 255
    ```
    _Spawns an Anubis with level 255!_

## /spawnpal_j { .toc-only }
??? info "/spawnpal_j"
    **语法:**

    Any of the following works:

    - `/spawnpal_j <PalTemplate>`
    - `/spawnpal <PalTemplate> [x] [y] [z]`

    **描述:** 按相对或绝对坐标生成一只帕鲁。**RCON 必须指定 x、y 和 z！**

    **Note:** All stats, except level, are randomized.

    **参数:**

    - `<PalTemplate>`: 要使用的 PalTemplate 文件名。
    - `[x]`: （可选）Pal 的 X 坐标。默认：相对于执行命令的玩家。
    - `[y]`: （可选）Pal 的 Y 坐标。默认：相对于执行命令的玩家。
    - `[z]`: （可选）Pal 的 Z 坐标。默认：相对于执行命令的玩家。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /spawnpal Anubis 255
    ```
    _Spawns an Anubis with level 255!_

## /summon { .toc-only }
??? info "/summon"
    **语法:** `/summon <PalSummon>`

    **描述:** 使用指定的 PalSummon 文件生成帕鲁。

    **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

    **参数:**
    - `<PalSummon>`: 要使用的 PalSummon 文件名。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /summon PalSummon
    ```

## /giveegg { .toc-only }
??? info "/giveegg"
    **语法:** `/giveegg <UserId> <EggId> <PalId> [Level]`

    **描述:** 给目标用户一个包含指定帕鲁的帕鲁蛋，并可选择调整等级。

    **参数:**

    ??? quote "<UserId\>"
        **描述:** 接收帕鲁蛋的玩家 ID。

    ??? quote "<EggId\>"
        **描述:** 要给予的蛋类型。

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
        **描述:** 蛋中包含的帕鲁。

        **Note:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。

    ??? quote "[Level\]"
        **描述:** （可选）蛋中帕鲁的等级。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
    ```


## /givemeegg { .toc-only }
??? info "/givemeegg"
    **语法:** `/givemeegg <EggId> <PalId> [Level]`

    **描述:** 给自己一个包含指定帕鲁的帕鲁蛋，并可选择调整等级。

    **参数:**

    ??? quote "<EggId\>"
        **描述:** 要给自己的蛋类型。

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
        **描述:** 蛋中包含的帕鲁。

        **Note:** 使用 Pal ID，例如 `WeaselDragon`（Chillet）。完整列表见 [paldeck.cc/pals](https://paldeck.cc/pals)。

    ??? quote "[Level]"
        **描述:** （可选）蛋中帕鲁的等级。

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /givemeegg PalEgg_Ice_01 WeaselDragon 10
    ```

## /giveegg_j { .toc-only }
??? info "/giveegg_j"
    **语法:** `/giveegg_j <EggId> <PalTemplate> [Level]`

    **描述:** 给出一个帕鲁蛋，内部帕鲁由 PalTemplate 文件定义，并可选择调整等级。

    **参数:**

    ??? quote "<EggId\>"
        **描述:** 要给予的蛋类型。

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
        **描述:** 要使用的 PalTemplate 文件名。

        **注意：** 文件名不需要包含 .json 扩展名；如果缺失，系统会自动追加。参见 [PalTemplate](../FileTypes/PalTemplate.md)。

    ??? quote "[Level]"
        **描述:** （可选）蛋中帕鲁的等级。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
    ```

## /givemeegg_j { .toc-only }
??? info "/givemeegg_j"
    **语法:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

    **描述:** 给自己一个帕鲁蛋，内部帕鲁由 PalTemplate 文件定义，并可选择调整等级。

    **参数:**

    ??? quote "<EggI\>"
        **描述:** 要给自己的蛋类型。

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
        **描述:** 要使用的 PalTemplate 文件名。

        **注意：** 文件名不需要包含 .json 扩展名；如果缺失，系统会自动追加。参见 [PalTemplate](../FileTypes/PalTemplate.md)。

    ??? quote "[Level]"
        **描述:** （可选）蛋中帕鲁的等级。

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
    ```

## /jetragon { .toc-only }
??? info "/jetragon"
    **语法:** `/jetragon`

    **描述:** 给你一只管理员空涡龙帕鲁（它飞得太快了……）。

    **参数:**
    - None

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /jetragon
    ```

## /catwaifu { .toc-only }
??? info "/catwaifu"
    **语法:** `/catwaifu`

    **描述:** 给你一只管理员猫娘帕鲁，用于增强角色属性。

    **参数:**

    - None

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /catwaifu
    ```

## /exportpals { .toc-only }
??? info "/exportpals"
    **语法:** `/exportpals [UserId]`

    **描述:** 将玩家的每只帕鲁导出为 PalTemplate 文件，位置为 Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/。

    **参数:**

    - `[UserId]`: （可选）要导出帕鲁的玩家 ID。省略时导出你自己的帕鲁。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /exportpals steam_76500000000000000
    /exportpals
    ```

## /deletepals { .toc-only }
??? info "/deletepals"
    **语法:** `/deletepals <UserId> <PalFilter>`

    **描述:** 使用高级过滤器删除指定用户的帕鲁。过滤器允许在一个命令中指定多个条件，例如 Pal ID、等级、性别、被动技能等。用于重要数据前请先在安全环境中测试。

    **参数:**

    ??? quote "<UserId\>"
        **描述:** 其帕鲁将被删除的玩家 ID。

    ??? quote "<PalFilter\>"
        **描述:** 用于选择要删除哪些帕鲁的一组过滤关键字。

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

        **示例过滤器：**

        - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
        - `ID Anubis Rank>=3`
        - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

        For more details, see the [PalFilter documentation](https://github.com/Ultimeit/PalDefender/blob/master/Wiki/Commands/deletepals.md).

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
    /deletepals 76567890987654321 ID Anubis Rank>=3
    /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
    ```







