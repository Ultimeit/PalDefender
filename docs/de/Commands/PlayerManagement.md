# Player Management

## /kick { .toc-only }
??? info "/kick"
    **Syntax:** `/kick <UserId> [Reason="Kicked by Admin."]`

    **Beschreibung:** Kickt einen Spieler vom Server.

    **Argumente:**

    - `<UserId>`: Die ID des zu kickenden Spielers.
    - `[Reason]`: (Optional) Grund für den Kick. Standard: "Kicked by Admin."

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /kick steam_76500000000000000 "Spamming in chat"
    ```

## /ban { .toc-only }
??? info "/ban"
    **Syntax:** `/ban <UserId> [Reason="Banned by Admin."]`

    **Beschreibung:** Bannt und kickt einen Spieler vom Server.

    **Argumente:**

    - `<UserId>`: Die ID des zu bannenden Spielers.
    - `[Reason]`: (Optional) Grund für den Bann. Standard: "Banned by Admin."

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /ban gdk_25300000000000000 "Cheating"
    ```

## /ipban { .toc-only }
??? info "/ipban"
    **Syntax:** `/ipban <UserId> [Reason="Banned by Admin."]`

    **Beschreibung:** Bannt die IP-Adresse eines Spielers und kickt ihn anschließend vom Server.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, dessen IP gebannt wird.
    - `[Reason]`: (Optional) Grund für den Bann. Standard: "Banned by Admin."

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /ipban steam_76500000000000000
    ```

## /banip { .toc-only }
??? info "/banip"
    **Syntax:** `/banip <IP>`

    **Beschreibung:** Bannt eine IP-Adresse vom Server.

    **Argumente:**

    - `<IP>`: Die zu bannende IP-Adresse.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /banip 192.168.1.1
    ```

## /unbanip { .toc-only }
??? info "/unbanip"
    **Syntax:** `/unbanip <IP>`

    **Beschreibung:** Entfernt eine IP-Adresse aus der Bannliste.

    **Argumente:**

    - `<IP>`: Die zu entbannende IP-Adresse.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /unbanip 192.168.1.1
    ```

## /unban { .toc-only }
??? info "/unban"
    **Syntax:** `/unban <UserId> [Reason="Unbanned by admin."]`

    **Beschreibung:** Entfernt eine UserId aus der PalDefender-Bannliste.

    **Argumente:**

    - `<UserId>`: Die zu entbannende UserId.
    - `[Reason]`: (Optional) Grund, der für die Entbannung gespeichert wird.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /unban steam_76500000000000000 "Appeal accepted"
    ```

## /getip { .toc-only }
??? info "/getip"
    **Syntax:** `/getip <UserId>`

    **Beschreibung:** Zeigt die IP-Adresse eines Spielers an.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /getip gdk_25300000000000000
    ```

## /whitelist_add { .toc-only }
??? info "/whitelist_add"
    **Syntax:** `/whitelist_add <UserId>`

    **Beschreibung:** Fügt eine UserId zur Whitelist hinzu.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers für die Whitelist.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /whitelist_add steam_76500000000000000
    ```

## /whitelist_remove { .toc-only }
??? info "/whitelist_remove"
    **Syntax:** `/whitelist_remove <UserId>`

    **Beschreibung:** Entfernt eine UserId aus der Whitelist.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der von der Whitelist entfernt wird.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /whitelist_remove gdk_25300000000000000
    ```

## /whitelist_get { .toc-only }
??? info "/whitelist_get"
    **Syntax:** `/whitelist_get`

    **Beschreibung:** Zeigt die vollständige Liste der Spieler auf der Whitelist.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /whitelist_get
    ```

## /imcheater { .toc-only }
??? info "/imcheater"
    **Syntax:** `/imcheater`

    **Beschreibung:** Damit kannst du testen, wie dein Server auf einen Cheater reagiert.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /imcheater
    ```

## /spectate { .toc-only }
??? info "/spectate"
    **Syntax:** `/spectate`

    **Beschreibung:** Aktiviert den Zuschauermodus. Entspricht dem Hotkey `\`, der jedoch nicht bei allen Spielern funktioniert, zum Beispiel auf Konsolen.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /spectate
    ```






