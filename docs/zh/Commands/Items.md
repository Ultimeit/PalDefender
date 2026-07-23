# Items

## /give { .toc-only }
??? info "/give"
    **语法:** `/give <UserId> <ItemId> [Amount=1]`

    **描述:** 给玩家一个物品，并可指定数量。

    **参数:**

    - `<UserId>`: 接收物品的玩家 ID。
    - `<ItemId>`: 要给予的物品。
    - `[Amount]`: （可选）数量。默认：1。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /give steam_76500000000000000 Sword 2
    ```

## /giveitems { .toc-only }
??? info "/giveitems"
    **语法:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

    **描述:** 在一个命令中给玩家多个物品，可用冒号为每个物品指定数量。

    **参数:**

    - `<UserId>`: 接收物品的玩家 ID。
    - `<ItemId>[:<Amount>] ...`: List of items and optional amounts.

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /giveitems gdk_25300000000000000 Sword:2 Shield:1
    ```

## /giveme { .toc-only }
??? info "/giveme"
    **语法:** `/giveme <ItemId> [Amount=1]`

    **描述:** 给自己一个物品，并可指定数量。

    **参数:**

    - `<ItemId>`: 要给自己的物品。
    - `[Amount]`: （可选）数量。默认：1。

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /giveme Sword 3
    ```

## /delitem { .toc-only }
??? info "/delitem"
    **语法:** `/delitem <UserId> <ItemId> [Amount=1]`

    **描述:** 从玩家身上删除物品，并可指定数量。默认值为 `1`，只删除一个。使用 `all` 替代 `1` 可删除全部。

    **参数:**

    - `<UserId>`: 玩家的 ID。
    - `<ItemId>`: 要删除的物品。
    - `[Amount]`：（可选）数量。默认：1。使用 `all` 删除所有匹配项。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /delitem steam_76500000000000000 Sword 1
    /delitem gdk_25300000000000000 Sword all
    ```

## /give_relic { .toc-only }
??? info "/give_relic"
    **语法:** `/give_relic <UserId> <RelicType> [Amount]`

    **描述:** 给玩家一个或多个指定类型的遗物点数。

    **参数:**

    - `<UserId>`: 接收遗物点数的玩家 ID。
    - `<RelicType>`: 要授予的遗物类型。

    - `[Amount]`: 可选的遗物点数数量，默认值为 `1`。

    **支持的遗物类型:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /give_relic steam_76500000000000000 CapturePower 5
    ```

## /giveme_relic { .toc-only }
??? info "/giveme_relic"
    **语法:** `/giveme_relic <RelicType> [Amount]`

    **描述:** 给自己一个或多个指定类型的遗物点数。

    **参数:**

    - `<RelicType>`: 要授予的遗物类型。

    - `[Amount]`: 给自己的可选遗物点数数量，默认值为 `1`。

    **支持的遗物类型:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /giveme_relic CapturePower 5
    ```


## /delitems { .toc-only }
??? info "/delitems"
    **语法:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

    **描述:** 在一个命令中从玩家身上删除多个物品，可用冒号指定每种物品的数量。使用 `all` 替代 `1` 可删除全部。

    **参数:**

    - `<UserId>`: 玩家的 ID。
    - `<ItemId>[:<Amount>] ...`: List of items and optional amounts.

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /delitems steam_76500000000000000 Sword:1 Shield:all
    ```

## /clearinv { .toc-only }
??? info "/clearinv"
    **语法:** `/clearinv <UserId> [Container=items] ...`

    **描述:** 清空玩家背包中的指定容器。可用容器包括 `items`、`keyitems`、`armor`、`weapons`、`food`、`dropslot` 或 `all`。

    **参数:**

    - `<UserId>`: 玩家的 ID。
    - `[Container] ...`: （可选）要清空的容器。默认：items。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /clearinv steam_76500000000000000 items
    /clearinv gdk_25300000000000000 all
    ```







