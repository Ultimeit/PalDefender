# Research Tree

## /learntech { .toc-only }
??? info "/learntech"
    **Syntax:** `/learntech <UserId> <TechID>`

    **Beschreibung:** Lässt einen Spieler eine bestimmte Technologie lernen. Nutze `all`, um alles freizuschalten.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `<TechID>`: Die zu lernende Technologie. Nutze `all`, um alles freizuschalten.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /learntech steam_76500000000000000 Tech001
    /learntech gdk_25300000000000000 all
    ```

## /unlearntech { .toc-only }
??? info "/unlearntech"
    **Syntax:** `/unlearntech <UserId> <TechID>`

    **Beschreibung:** Lässt einen Spieler eine bestimmte Technologie vergessen. Nutze `all`, um alles zu entfernen.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `<TechID>`: Die zu vergessende Technologie. Nutze `all`, um alles zu entfernen.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /unlearntech gdk_25300000000000000 Tech001
    /unlearntech steam_76500000000000000 all
    ```

## /givetechpoints { .toc-only }
??? info "/givetechpoints"
    **Syntax:** `/givetechpoints <UserId> [Amount=1]`

    **Beschreibung:** Gibt dem Zielbenutzer X Technologiepunkte.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der Technologiepunkte erhalten soll.
    - `[Amount]`: (Optional) Anzahl der zu gebenden Technologiepunkte. Standard: 1.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /givetechpoints steam_76500000000000000 10
    ```

## /givebosstechpoints { .toc-only }
??? info "/givebosstechpoints"
    **Syntax:** `/givebosstechpoints <UserId> [Amount=1]`

    **Beschreibung:** Gibt dem Zielbenutzer X Antike-Technologiepunkte.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der Antike-Technologiepunkte erhalten soll.
    - `[Amount]`: (Optional) Anzahl der zu gebenden Antike-Technologiepunkte. Standard: 1.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /givebosstechpoints steam_76500000000000000 5
    ```

## /givemetechpoints { .toc-only }
??? info "/givemetechpoints"
    **Syntax:** `/givemetechpoints [Amount=1]`

    **Beschreibung:** Gibt dir selbst X Technologiepunkte.

    **Argumente:**

    - `[Amount]`: (Optional) Anzahl der Technologiepunkte für dich selbst. Standard: 1.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /givemetechpoints 10
    ```

## /givemebosstechpoints { .toc-only }
??? info "/givemebosstechpoints"
    **Syntax:** `/givemebosstechpoints [Amount=1]`

    **Beschreibung:** Gibt dir selbst X Antike-Technologiepunkte.

    **Argumente:**

    - `[Amount]`: (Optional) Anzahl der Antike-Technologiepunkte für dich selbst. Standard: 1.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /givemebosstechpoints 5
    ```







