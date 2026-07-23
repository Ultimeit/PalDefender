# Base Management

## /getnearestbase { .toc-only }
??? info "/getnearestbase"
    **语法:** `/getnearestbase [X] [Y] [Z]`

    **描述:** 显示离你角色最近的基地所属公会名称。

    **Note:** When executed via **RCON**, all location parameters (`[X]` `[Y]` `[Z]`) **are required**, since RCON has no player character to determine the location.

    **参数:**

    - `[X]`: （可选）X 坐标。
    - `[Y]`: （可选）Y 坐标。
    - `[Z]`: （可选）Z 坐标。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /getnearestbase 100 200 50
    ```

## /gotonearestbase { .toc-only }
??? info "/gotonearestbase"
    **语法:** `/gotonearestbase [X] [Y] [Z]`

    **描述:** 将你传送到当前位置附近最近的基地。

    **Note:** When executed via **RCON**, all location parameters (`[X]` `[Y]` `[Z]`) **are required**, since RCON has no player character to determine the location.

    **参数:**

    - `[X]`: （可选）X 坐标。
    - `[Y]`: （可选）Y 坐标。
    - `[Z]`: （可选）Z 坐标。

    **权限:** `Chat`, `Admin`

    **示例:**
    ```
    /gotonearestbase 100 200 50
    ```

## /killnearestbase { .toc-only }
??? info "/killnearestbase"
    **语法:** `/killnearestbase [X] [Y] [Z]`

    **描述:** 摧毁最近的基地（**请谨慎使用！**）。

    **Note:** When executed via **RCON**, all location parameters (`[X]` `[Y]` `[Z]`) **are required**, since RCON has no player character to determine the location.

    **参数:**

    - `[X]`: （可选）X 坐标。
    - `[Y]`: （可选）Y 坐标。
    - `[Z]`: （可选）Z 坐标。

    **权限:** `Chat`, `RCON`, `Admin`

    **示例:**
    ```
    /killnearestbase 100 200 50
    ```







