# Server Management

## /version { .toc-only }
??? info "/version"
    **Syntax:** `/version`

    **Beschreibung:** Zeigt die Palworld-Spielversion und die PalDefender-Version. RCON liefert JSON-Ausgabe zurück.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /version
    ```

## /reloadcfg { .toc-only }
??? info "/reloadcfg"
    **Syntax:** `/reloadcfg`

    **Beschreibung:** Lädt `Config.json`, `WhiteList.json` und PalDefender-Bandaten neu.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /reloadcfg
    ```

## /addadminip { .toc-only }
??? info "/addadminip"
    **Syntax:** `/addadminip <IP>`

    **Beschreibung:** Fügt der Admin-Whitelist eine IP-Adresse hinzu.

    **Argumente:**

    - `<IP>`: Die IP-Adresse, die als Admin hinzugefügt wird.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /addadminip 192.168.1.1
    ```

## /setadmin { .toc-only }
??? info "/setadmin"
    **Syntax:** `/setadmin <UserId>`

    **Beschreibung:** Erteilt oder entzieht einem Spieler temporär Adminrechte.

    **Argumente:**

    - `<UserId>`: Die ID des Spielers, dem Adminrechte erteilt/entzogen werden.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /setadmin steam_76500000000000000
    ```

## /pgbroadcast { .toc-only }
??? info "/pgbroadcast"
    **Syntax:** `/pgbroadcast <Message>`

    **Beschreibung:** Sendet eine Nachricht an alle Spieler auf dem Server.

    **Argumente:**

    - `<Message>`: Die zu sendende Broadcast-Nachricht.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /pgbroadcast "Server will restart soon."
    ```

## /adminlogin { .toc-only }
??? info "/adminlogin"
    **Syntax:** `/adminlogin <password>`

    **Beschreibung:** Meldet dich im Adminmodus an. Benötigt dein Adminpasswort als Argument.

    **Argumente:**

    - `<password>`: Das Adminpasswort.

    **Berechtigungen:** `Chat`

    **Beispiel:**
    ```
    /adminlogin mySecretPassword
    ```

## /adminlogout { .toc-only }
??? info "/adminlogout"
    **Syntax:** `/adminlogout`

    **Beschreibung:** Meldet dich aus dem Adminmodus ab.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /adminlogout
    ```

## /iwantplayerlist { .toc-only }
??? info "/iwantplayerlist"
    **Syntax:** `/iwantplayerlist`

    **Beschreibung:** Aktiviert das Spielerlisten-Overlay im Spiel, sodass du beim Drücken von ESC die UserId und Player UID jedes Spielers sehen kannst. Nützlich für Serveradmins und Spieler, die detaillierte Spielerinformationen direkt im Spiel sehen möchten.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /iwantplayerlist
    ```

## /getpos { .toc-only }
??? info "/getpos"
    **Syntax:** `/getpos [UserId]`

    **Beschreibung:** Zeigt deine aktuelle Weltposition an, die für Teleports, Beschwörungen und ähnliche Aktionen genutzt werden kann. Wenn eine [UserId] angegeben wird, wird stattdessen die Position dieses Spielers ausgegeben.

    **Argumente:**

    - `[UserId]`: (Optional) Die ID des Spielers, dessen Position du abrufen willst. Wenn weggelassen, wird deine eigene Position abgerufen.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /getpos
    /getpos steam_76500000000000000
    ```

## /settime { .toc-only }
??? info "/settime"
    **Syntax:** `/settime <hour>`

    **Beschreibung:** Ändert die Zeit in Palworld. Die Stunde kann Werte von `0` bis `23` sowie `day` und `night` haben.

    **Argumente:**

    - `<hour>`: Hour value (0-23, day, night).

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /settime 12
    /settime night
    ```

## /togglepvp { .toc-only }
??? info "/togglepvp"
    **Syntax:** `/togglepvp`

    **Beschreibung:** Schaltet Server-PvP für die laufende Sitzung ein oder aus.

    **Argumente:**

    - None

    **Berechtigungen:** `Chat`, `Admin`

    **Beispiel:**
    ```
    /togglepvp
    ```

## /alert { .toc-only }
??? info "/alert"
    **Syntax:** `/alert <message>`

    **Beschreibung:** Sendet eine Warnmeldung an alle Spieler auf dem Server. Diese Nachricht wird normalerweise gut sichtbar auf dem Bildschirm angezeigt.

    **Argumente:**

    - `<message>`: Die Nachricht, die als Warnung gesendet wird.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /alert Server will restart in 5 minutes!
    ```

## /send { .toc-only }
??? info "/send"
    **Syntax:** `/send <type> <UserId> <Message>`

    **Beschreibung:** Ermöglicht das Senden einer Nachricht oder Lognachricht an einen bestimmten Spieler.

    **Argumente:**

    - `<type>`: Der Typ der zu sendenden Nachricht. Mögliche Werte:
         - `msg`: Regular chat message.
         - `log`: Regular log message (white, disappears quickly, larger font).
         - `ilog`: Important log message (blue, stays longer).
         - `vilog`: Very important log message (blue, stays extremely long).
    - `<UserId>`: Die ID des Spielers, der die Nachricht erhalten soll.
    - `<Message>`: Der zu sendende Nachrichtentext.

    **Berechtigungen:** `Chat`, `RCON`, `Admin`

    **Beispiel:**
    ```
    /send msg steam_76500000000000000 Dont miss out on Qonzer's sale!
    /send log steam_76500000000000000 Dont miss out on Qonzer's sale!
    /send ilog steam_76500000000000000 Dont miss out on Qonzer's sale!
    /send vilog steam_76500000000000000 Dont miss out on Qonzer's sale!
    ```






