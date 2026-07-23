# Items

## /give { .toc-only }
??? info "/give"
    **Syntax:** `/give <UserId> <ItemId> [Amount=1]`

    **Beschreibung:** Gibt einem Spieler ein Item und optional eine bestimmte Anzahl.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der das Item erhalten soll.
    - `<ItemId>`: Das zu gebende Item.
    - `[Amount]`: (Optional) Anzahl. Standard: 1.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /give steam_76500000000000000 Sword 2
    ```

## /giveitems { .toc-only }
??? info "/giveitems"
    **Syntax:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

    **Beschreibung:** Gibt einem Spieler mehrere Items mit einem Befehl; Mengen können pro Item mit Doppelpunkt angegeben werden.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der die Items erhalten soll.
    - `<ItemId>[:<Amount>] ...`: List of items and optional amounts.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /giveitems gdk_25300000000000000 Sword:2 Shield:1
    ```

## /giveme { .toc-only }
??? info "/giveme"
    **Syntax:** `/giveme <ItemId> [Amount=1]`

    **Beschreibung:** Gibt dir selbst ein Item und optional eine bestimmte Anzahl.

    **Argumente:**

    - `<ItemId>`: Das Item, das du dir selbst gibst.
    - `[Amount]`: (Optional) Anzahl. Standard: 1.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /giveme Sword 3
    ```

## /delitem { .toc-only }
??? info "/delitem"
    **Syntax:** `/delitem <UserId> <ItemId> [Amount=1]`

    **Beschreibung:** Löscht ein Item bei einem Spieler und optional eine bestimmte Anzahl. Standard ist `1`, wodurch nur ein Exemplar gelöscht wird. Nutze `all` statt `1`, um alle Exemplare zu löschen.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `<ItemId>`: Das zu löschende Item.
    - `[Amount]`: (Optional) Anzahl. Standard: 1. Nutze `all`, um alle Vorkommen zu löschen.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /delitem steam_76500000000000000 Sword 1
    /delitem gdk_25300000000000000 Sword all
    ```

## /give_relic { .toc-only }
??? info "/give_relic"
    **Syntax:** `/give_relic <UserId> <RelicType> [Amount]`

    **Beschreibung:** Gibt dem Spieler einen oder mehrere Reliktpunkte des ausgewählten Typs.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der die Reliktpunkte erhalten soll.
    - `<RelicType>`: Der zu gewährende Relikt-Typ.

    - `[Amount]`: Optionale Anzahl der zu gewährenden Reliktpunkte. Standard ist `1`.

    **Unterstützte Relikt-Typen:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /give_relic steam_76500000000000000 CapturePower 5
    ```

## /giveme_relic { .toc-only }
??? info "/giveme_relic"
    **Syntax:** `/giveme_relic <RelicType> [Amount]`

    **Beschreibung:** Gibt dir selbst einen oder mehrere Reliktpunkte des ausgewählten Typs.

    **Argumente:**

    - `<RelicType>`: Der zu gewährende Relikt-Typ.

    - `[Amount]`: Optionale Anzahl der Reliktpunkte, die du dir selbst gibst. Standard ist `1`.

    **Unterstützte Relikt-Typen:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /giveme_relic CapturePower 5
    ```


## /delitems { .toc-only }
??? info "/delitems"
    **Syntax:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

    **Beschreibung:** Löscht mehrere Items eines Spielers mit einem Befehl; Mengen können pro Item mit Doppelpunkt angegeben werden. Nutze `all` statt `1`, um alle Exemplare zu löschen.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `<ItemId>[:<Amount>] ...`: List of items and optional amounts.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /delitems steam_76500000000000000 Sword:1 Shield:all
    ```

## /clearinv { .toc-only }
??? info "/clearinv"
    **Syntax:** `/clearinv <UserId> [Container=items] ...`

    **Beschreibung:** Leert angegebene Container im Inventar eines Spielers. Verfügbare Container: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot` oder `all`.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `[Container] ...`: (Optional) Zu leerende Container. Standard: items.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /clearinv steam_76500000000000000 items
    /clearinv gdk_25300000000000000 all
    ```







