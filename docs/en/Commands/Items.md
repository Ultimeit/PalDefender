# Items

## /give { .toc-only }
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

## /giveitems { .toc-only }
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

## /giveme { .toc-only }
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

## /delitem { .toc-only }
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

## /give_relic { .toc-only }
??? info "/give_relic"
    **Syntax:** `/give_relic <UserId> <RelicType> [Amount]`

    **Description:** Gives the player one or more relic points of the selected type.

    **Arguments:**

    - `<UserId>`: The ID of the player to receive the relic points.
    - `<RelicType>`: The relic type to grant.

    - `[Amount]`: Optional number of relic points to give. Defaults to `1`.

    **Supported relic types:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

    **Permissions:** `Chat`, `RCON`, `Admin`

    **Example:**
    ```
    /give_relic steam_76500000000000000 CapturePower 5
    ```

## /giveme_relic { .toc-only }
??? info "/giveme_relic"
    **Syntax:** `/giveme_relic <RelicType> [Amount]`

    **Description:** Gives yourself one or more relic points of the selected type.

    **Arguments:**

    - `<RelicType>`: The relic type to grant.

    - `[Amount]`: Optional number of relic points to give yourself. Defaults to `1`.

    **Supported relic types:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

    **Permissions:** `Chat`, `Admin`

    **Example:**
    ```
    /giveme_relic CapturePower 5
    ```


## /delitems { .toc-only }
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

## /clearinv { .toc-only }
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







