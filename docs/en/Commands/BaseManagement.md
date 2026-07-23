# Base Management

## /getnearestbase { .toc-only }
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

## /gotonearestbase { .toc-only }
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

## /killnearestbase { .toc-only }
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







