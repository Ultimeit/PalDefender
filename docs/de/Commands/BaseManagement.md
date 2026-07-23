# Base Management

## /getnearestbase { .toc-only }
??? info "/getnearestbase"
    **Syntax:** `/getnearestbase [X] [Y] [Z]`

    **Beschreibung:** Zeigt den Gildennamen der Basis an, die deinem Charakter am nächsten ist.

    **Hinweis:** Bei Ausführung über **RCON** sind alle Positionsparameter (`[X]` `[Y]` `[Z]`) **erforderlich**, da RCON keinen Spielercharakter hat, aus dem eine Position abgeleitet werden kann.

    **Argumente:**

    - `[X]`: (Optional) X-Koordinate.
    - `[Y]`: (Optional) Y-Koordinate.
    - `[Z]`: (Optional) Z-Koordinate.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /getnearestbase 100 200 50
    ```

## /gotonearestbase { .toc-only }
??? info "/gotonearestbase"
    **Syntax:** `/gotonearestbase [X] [Y] [Z]`

    **Beschreibung:** Teleportiert dich zur nächstgelegenen Basis am Standort.

    **Hinweis:** Bei Ausführung über **RCON** sind alle Positionsparameter (`[X]` `[Y]` `[Z]`) **erforderlich**, da RCON keinen Spielercharakter hat, aus dem eine Position abgeleitet werden kann.

    **Argumente:**

    - `[X]`: (Optional) X-Koordinate.
    - `[Y]`: (Optional) Y-Koordinate.
    - `[Z]`: (Optional) Z-Koordinate.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /gotonearestbase 100 200 50
    ```

## /killnearestbase { .toc-only }
??? info "/killnearestbase"
    **Syntax:** `/killnearestbase [X] [Y] [Z]`

    **Beschreibung:** Zerstört die nächstgelegene Basis (**mit Vorsicht verwenden!**).

    **Hinweis:** Bei Ausführung über **RCON** sind alle Positionsparameter (`[X]` `[Y]` `[Z]`) **erforderlich**, da RCON keinen Spielercharakter hat, aus dem eine Position abgeleitet werden kann.

    **Argumente:**

    - `[X]`: (Optional) X-Koordinate.
    - `[Y]`: (Optional) Y-Koordinate.
    - `[Z]`: (Optional) Z-Koordinate.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /killnearestbase 100 200 50
    ```







