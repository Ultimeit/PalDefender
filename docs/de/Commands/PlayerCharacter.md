# Player Character

## /tp { .toc-only }
??? info "/tp"
    **Syntax:**
    Any of the following works:

    - `/tp <UserId>`
    - `/tp <UserId1> <UserId2>`
    - `/tp <X> <Y>`
    - `/tp <X> <Y> <Z>`
    - `/tp <UserId> <X> <Y>`
    - `/tp <UserId> <X> <Y> <Z>`
    - `/tp home`
    - `/tp oilrig`
    - `/tp oilrig:Lv30`
    - `/tp oilrig:Lv55`
    - `/tp oilrig:Lv60`

    **Beschreibung:** Teleportiert dich oder einen angegebenen Spieler zu einem anderen Spieler, Koordinaten, der nächsten eigenen Basis oder einem Ölturm-Ziel.

    **Note:** RCON must include the player being teleported because RCON has no in-game character.

    **Argumente:**

    - `<UserId>`: A player to teleport to, or the player being teleported when more arguments are supplied.
    - `<UserId1>`: Der Spieler, der teleportiert wird.
    - `<UserId2>`: Der Zielspieler.
    - `<X> <Y> [Z]`: Kartenkoordinaten. Wenn `Z` weggelassen wird, versucht PalDefender eine nutzbare Bodenhöhe zu finden.
    - `home`: Teleports to the nearest owned base.
    - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60`: Teleports to an oilrig destination.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /tp steam_76500000000000000 gdk_25300000000000000
    /tp 100 -250
    /tp oilrig:Lv60
    ```

## /give_exp { .toc-only }
??? info "/give_exp"
    **Syntax:** `/give_exp <UserId> <Amount>`

    **Beschreibung:** Gibt einem Spieler Erfahrungspunkte.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `<Amount>`: Amount of experience points.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /give_exp gdk_25300000000000000 1000
    ```

## /giveme_exp { .toc-only }
??? info "/giveme_exp"
    **Syntax:** `/giveme_exp <Amount>`

    **Beschreibung:** Gibt dir selbst Erfahrungspunkte.

    **Argumente:**

    - `<Amount>`: Amount of experience points.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /giveme_exp 1000
    ```

## /renameplayer { .toc-only }
??? info "/renameplayer"
    **Syntax:** `/renameplayer <UserId> <NewName>`

    **Beschreibung:** Ändert den Spitznamen eines Spielers.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers.
    - `<NewName>`: Der neue Spitzname.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /renameplayer steam_76500000000000000 NewNickname
    ```

## /givestats { .toc-only }
??? info "/givestats"
    **Syntax:** `/givestats <UserId> [Count=1]`

    **Beschreibung:** Gibt dem Spieler einen oder mehrere ungenutzte Statuspunkte; negative Werte ziehen Punkte ab. Bereits verteilte Punkte werden nicht beeinflusst.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, der die Statuspunkte erhalten soll.
    - `[Count]`: (Optional) Anzahl der ungenutzten Statuspunkte; negative Werte ziehen ab. Standard: 1.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /givestats steam_76500000000000000 5
    /givestats steam_76500000000000000 -2
    ```

## /givemestats { .toc-only }
??? info "/givemestats"
    **Syntax:** `/givemestats [Count=1]`

    **Beschreibung:** Gibt dir selbst einen oder mehrere ungenutzte Statuspunkte; negative Werte ziehen Punkte ab. Bereits verteilte Punkte werden nicht beeinflusst.

    **Argumente:**

    - `[Count]`: (Optional) Anzahl der ungenutzten Statuspunkte für dich selbst; negative Werte ziehen ab. Standard: 1.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /givemestats 5
    /givemestats -2
    ```

## /godmode { .toc-only }
??? info "/godmode"
    **Syntax:** `/godmode [on/off]`

    **Beschreibung:** Gewährt Unverwundbarkeit inklusive Immunität gegen Statuseffekte, verhindert Nahrungsverbrauch und stellt beim Aktivieren Gesundheit wieder her. Optional kann alles mit einem Treffer getötet werden, wenn dies in der Config aktiviert ist.

    **Argumente:**

    - `[on/off]`: (Optional) Aktiviert oder deaktiviert Godmode explizit. Standard: Umschalten.

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /godmode
    /godmode on
    /godmode off
    ```






