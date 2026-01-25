# Befehle

## Was sind Befehle?

Befehle sind spezielle textbasierte Anweisungen, mit denen du mit dem Spiel interagieren kannst. Durch das Eingeben von Befehlen im Chat kannst du Aktionen wie Teleportieren, das Erzeugen von Kreaturen oder die Verwaltung von Spielern ausführen. Befehle beginnen in der Regel mit einem <span class="var-command">/</span>, gefolgt vom Befehlsnamen und optionalen Argumenten.

## Wer kann Befehle verwenden?

**Derzeit gibt es keinen Befehl, der von Nicht-Admin-Spielern verwendet werden kann.**
In der aktuellen Version stehen ausschließlich Admin- und RCON-Befehle zur Verfügung.

## Befehlsliste

!!! note "Befehlssyntax"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → Muss angegeben werden.<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → Kann weggelassen werden. <span class="var-command-optional">{?}</span> gibt den Standardwert an, der verwendet wird, wenn das Argument fehlt.
    </p>
    <p>
    Argumente haben unterschiedliche Typen. Die häufigsten sind <span class="var-string">Strings</span>, <span class="var-number">Zahlen</span>, <span class="var-float">Floats</span> und <span class="var-bool">Booleans</span>. Einige Befehle verwenden komplexere Typen, z. B. bestimmte <span class="file">Dateinamen</span> in speziellen Verzeichnissen oder sogar einen <span class="var-filter">Filter</span>.
    </p>

??? note "Nur RCON"
    ??? info "/getrconcmds"
        **Syntax:** `/getrconcmds`

        **Beschreibung:** Gibt eine Liste aller Befehle zurück, inklusive der benötigten Argumentanzahl, die über RCON nutzbar sind.

        **Argumente:**

        - Keine

        **Berechtigungen:** `RCON`

        **Beispiel:**
        ```
        /getrconcmds
        ```

??? note "Serververwaltung"
    ??? info "/reloadcfg"
        **Syntax:** `/reloadcfg`

        **Beschreibung:** Lädt `Config.json`, `whitelist.json` und `banlist.txt` neu.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **Syntax:** `/addadminip <IP>`

        **Beschreibung:** Fügt eine IP-Adresse zur Admin-Whitelist hinzu.

        **Argumente:**

        - `<IP>`: Die IP-Adresse, die als Admin hinzugefügt werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **Syntax:** `/setadmin <UserId>`

        **Beschreibung:** Gewährt oder entzieht einem Spieler temporär Admin-Rechte.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **Syntax:** `/pgbroadcast <Message>`

        **Beschreibung:** Sendet eine Nachricht an alle Spieler auf dem Server.

        **Argumente:**

        - `<Message>`: Die zu sendende Nachricht.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /pgbroadcast "Server wird bald neu gestartet."
        ```

    ??? info "/adminlogin"
        **Syntax:** `/adminlogin <password>`

        **Beschreibung:** Meldet dich im Admin-Modus an. Erfordert das Admin-Passwort.

        **Argumente:**

        - `<password>`: Das Admin-Passwort.

        **Berechtigungen:** `Chat`

        **Beispiel:**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **Syntax:** `/adminlogout`

        **Beschreibung:** Meldet dich vom Admin-Modus ab.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /adminlogout
        ```


    ??? info "/iwantplayerlist"
        **Syntax:** `/iwantplayerlist`

        **Beschreibung:** Aktiviert das In-Game-Spielerliste-Overlay. Beim Drücken von ESC kannst du die UserId und Player UID aller Spieler sehen. Nützlich für Server-Admins und Spieler, die detaillierte Spielerinformationen direkt im Spiel einsehen möchten.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **Syntax:** `/getpos [UserId]`

        **Beschreibung:** Gibt deine aktuelle Position in der Welt zurück. Diese kann z. B. für Teleportation, Beschwörungen oder ähnliche Aktionen verwendet werden. Wenn eine [UserId] angegeben ist, wird stattdessen die Position dieses Spielers ausgegeben.

        **Argumente:**

        - `[UserId]`: (Optional) Die ID des Spielers, dessen Position abgefragt werden soll. Wird kein Wert angegeben, wird die eigene Position verwendet.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **Syntax:** `/settime <hour>`

        **Beschreibung:** Ändert die Zeit in Palworld. Der Wert für `<hour>` kann `0` bis `23`, `day` oder `night` sein.

        **Argumente:**

        - `<hour>`: Stundenwert (0–23, day, night).

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/alert"
        **Syntax:** `/alert <message>`

        **Beschreibung:** Sendet eine Alarmmeldung an alle Spieler auf dem Server. Diese Nachricht wird in der Regel prominent auf dem Bildschirm angezeigt.

        **Argumente:**

        - `<message>`: Die als Alarm zu sendende Nachricht.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /alert Server wird in 5 Minuten neu gestartet!
        ```

    ??? info "/send"
        **Syntax:** `/send <type> <UserId> <Message>`

        **Beschreibung:** Ermöglicht das Senden einer Nachricht oder Log-Nachricht an einen bestimmten Spieler.

        **Argumente:**

        - `<type>`: Typ der zu sendenden Nachricht. Mögliche Werte:
             - `msg`: Normale Chat-Nachricht.
             - `log`: Normale Log-Nachricht (weiß, verschwindet schnell, größere Schrift).
             - `ilog`: Wichtige Log-Nachricht (blau, bleibt länger sichtbar).
             - `vilog`: Sehr wichtige Log-Nachricht (blau, bleibt extrem lange sichtbar).
        - `<UserId>`: Die ID des Spielers, der die Nachricht erhalten soll.
        - `<Message>`: Der zu sendende Nachrichtentext.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /send msg steam_76500000000000000 Verpasse nicht den Qonzer-Sale!
        /send log steam_76500000000000000 Verpasse nicht den Qonzer-Sale!
        /send ilog steam_76500000000000000 Verpasse nicht den Qonzer-Sale!
        /send vilog steam_76500000000000000 Verpasse nicht den Qonzer-Sale!
        ```

??? note "Basenverwaltung"
    ??? info "/getnearestbase"
        **Syntax:** `/getnearestbase [X] [Y] [Z]`

        **Beschreibung:** Gibt den Gildennamen aus, dem die dem Spieler nächstgelegene Basis gehört.

        **Hinweis:** Bei Ausführung über **RCON** sind alle Positionsparameter (`[X]` `[Y]` `[Z]`) **zwingend erforderlich**, da RCON keinen Spielercharakter zur Positionsbestimmung hat.

        **Argumente:**

        - `[X]`: (Optional) X-Koordinate.
        - `[Y]`: (Optional) Y-Koordinate.
        - `[Z]`: (Optional) Z-Koordinate.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **Syntax:** `/gotonearestbase [X] [Y] [Z]`

        **Beschreibung:** Teleportiert dich zur nächstgelegenen Basis der angegebenen Position.

        **Hinweis:** Bei Ausführung über **RCON** sind alle Positionsparameter (`[X]` `[Y]` `[Z]`) **zwingend erforderlich**, da RCON keinen Spielercharakter zur Positionsbestimmung hat.

        **Argumente:**

        - `[X]`: (Optional) X-Koordinate.
        - `[Y]`: (Optional) Y-Koordinate.
        - `[Z]`: (Optional) Z-Koordinate.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **Syntax:** `/killnearestbase [X] [Y] [Z]`

        **Beschreibung:** Zerstört die nächstgelegene Basis (**mit Vorsicht verwenden!**).

        **Hinweis:** Bei Ausführung über **RCON** sind alle Positionsparameter (`[X]` `[Y]` `[Z]`) **zwingend erforderlich**, da RCON keinen Spielercharakter zur Positionsbestimmung hat.

        **Argumente:**

        - `[X]`: (Optional) X-Koordinate.
        - `[Y]`: (Optional) Y-Koordinate.
        - `[Z]`: (Optional) Z-Koordinate.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "Spielerverwaltung"
    ??? info "/kick"
        **Syntax:** `/kick <UserId> [Reason="Kicked by Admin."]`

        **Beschreibung:** Kickt einen Spieler vom Server.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, der gekickt werden soll.
        - `[Reason]`: (Optional) Grund für den Kick. Standard: "Kicked by Admin."

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /kick steam_76500000000000000 "Spamming im Chat"
        ```

    ??? info "/ban"
        **Syntax:** `/ban <UserId> [Reason="Banned by Admin."]`

        **Beschreibung:** Bannt einen Spieler und kickt ihn vom Server.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, der gebannt werden soll.
        - `[Reason]`: (Optional) Grund für den Bann. Standard: "Banned by Admin."

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /ban gdk_25300000000000000 "Cheaten"
        ```

    ??? info "/ipban"
        **Syntax:** `/ipban <UserId> [Reason="Banned by Admin."]`

        **Beschreibung:** Bannt die IP-Adresse eines Spielers und kickt ihn anschließend vom Server.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, dessen IP gebannt werden soll.
        - `[Reason]`: (Optional) Grund für den Bann. Standard: "Banned by Admin."

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **Syntax:** `/banip <IP>`

        **Beschreibung:** Bannt eine IP-Adresse vom Server.

        **Argumente:**

        - `<IP>`: Die IP-Adresse, die gebannt werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **Syntax:** `/unbanip <IP>`

        **Beschreibung:** Entfernt eine IP-Adresse aus der Bannliste.

        **Argumente:**

        - `<IP>`: Die IP-Adresse, die entbannt werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/getip"
        **Syntax:** `/getip <UserId>`

        **Beschreibung:** Zeigt dir die IP-Adresse eines Spielers an.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **Syntax:** `/whitelist_add <UserId>`

        **Beschreibung:** Fügt eine UserId zur Whitelist hinzu.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, der zur Whitelist hinzugefügt werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **Syntax:** `/whitelist_remove <UserId>`

        **Beschreibung:** Entfernt eine UserId aus der Whitelist.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, die aus der Whitelist entfernt werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **Syntax:** `/whitelist_get`

        **Beschreibung:** Zeigt die vollständige Liste aller Spieler auf der Whitelist an.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **Syntax:** `/imcheater`

        **Beschreibung:** Dient zum Testen, wie der Server auf einen Cheater reagiert.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **Syntax:** `/spectate`

        **Beschreibung:** Aktiviert den Spectate-Modus. Entspricht dem Drücken der Hotkey-Taste `\`. Der Hotkey funktioniert jedoch nicht bei allen Spielern (z. B. Konsolenspielern).

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /spectate
        ```

??? note "Spielercharakter"
    ??? info "/tp"
        **Syntax:** `/tp <UserId1> <UserId2>`

        **Beschreibung:** Teleportiert UserId1 zu UserId2.

        **Argumente:**

        - `<UserId1>`: Der Spieler, der teleportiert werden soll.
        - `<UserId2>`: Der Zielspieler.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        ```

    ??? info "/give_exp"
        **Syntax:** `/give_exp <UserId> <Amount>`

        **Beschreibung:** Vergibt Erfahrungspunkte an einen Spieler.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<Amount>`: Anzahl der Erfahrungspunkte.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **Syntax:** `/giveme_exp <Amount>`

        **Beschreibung:** Vergibt Erfahrungspunkte an dich selbst.

        **Argumente:**

        - `<Amount>`: Anzahl der Erfahrungspunkte.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **Syntax:** `/renameplayer <UserId> <NewName>`

        **Beschreibung:** Ändert den Nicknamen eines Spielers.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<NewName>`: Der neue Nickname.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /renameplayer steam_76500000000000000 NeuerName
        ```

    ??? info "/givestats"
        **Syntax:** `/givestats <UserId> [Count=1]`

        **Beschreibung:** Gibt einem Spieler einen oder mehrere ungenutzte Statuspunkte (negative Werte ziehen Punkte ab). Bereits verteilte Punkte bleiben unberührt.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `[Count]`: (Optional) Anzahl der zu vergebenden Statuspunkte (kann negativ sein). Standard: 1.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **Syntax:** `/givemestats [Count=1]`

        **Beschreibung:** Gibt dir selbst einen oder mehrere ungenutzte Statuspunkte (negative Werte ziehen Punkte ab). Bereits verteilte Punkte bleiben unberührt.

        **Argumente:**

        - `[Count]`: (Optional) Anzahl der zu vergebenden Statuspunkte (kann negativ sein). Standard: 1.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **Syntax:** `/godmode [on/off]`

        **Beschreibung:** Gewährt Unverwundbarkeit inklusive Immunität gegen Statuseffekte, verhindert den Verbrauch von Nahrung und stellt bei Aktivierung die Gesundheit wieder her. Optional kann One-Shot-Schaden aktiviert werden, sofern dies in der Konfiguration erlaubt ist.

        **Argumente:**

        - `[on/off]`: (Optional) Aktiviert oder deaktiviert den Godmode explizit. Standard: Umschalten ein/aus.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

??? note "Gildenverwaltung"
    ??? info "/setguildleader"
        **Syntax:** `/setguildleader <UserId>`

        **Beschreibung:** Macht den angegebenen Spieler zum Anführer seiner aktuellen Gilde.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, der Gildenanführer werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **Syntax:** `/exportguilds`

        **Beschreibung:** Exportiert alle Gilden des Servers in die Datei `Pal/Binaries/Win64/PalDefender/guildexport.json`.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /exportguilds
        ```
        Beispiel-Ausgabedatei: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "Items"
    ??? info "/give"
        **Syntax:** `/give <UserId> <ItemId> [Amount=1]`

        **Beschreibung:** Gibt einem Spieler ein Item und optional die angegebene Menge.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<ItemId>`: Das zu vergebende Item.
        - `[Amount]`: (Optional) Anzahl. Standard: 1.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **Syntax:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **Beschreibung:** Gibt einem Spieler mehrere Items in einem einzigen Befehl. Die Menge kann pro Item mit einem Doppelpunkt angegeben werden.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<ItemId>[:<Amount>] ...`: Liste von Items mit optionaler Mengenangabe.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **Syntax:** `/giveme <ItemId> [Amount=1]`

        **Beschreibung:** Gibt dir selbst ein Item und optional die angegebene Menge.

        **Argumente:**

        - `<ItemId>`: Das zu vergebende Item.
        - `[Amount]`: (Optional) Anzahl. Standard: 1.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **Syntax:** `/delitem <UserId> <ItemId> [Amount=1]`

        **Beschreibung:** Entfernt ein Item aus dem Inventar eines Spielers. Standardmäßig wird ein Item entfernt. Mit `all` werden alle Vorkommen gelöscht.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<ItemId>`: Das zu löschende Item.
        - `[Amount]`: (Optional) Anzahl. Standard: 1. Verwende `all`, um alle Vorkommen zu entfernen.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **Syntax:** `/give_relic <UserId> <Amount>`

        **Beschreibung:** Gibt einem Spieler eine oder mehrere Lifmunk-Effigien.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<Amount>`: Anzahl der Lifmunk-Effigien.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /give_relic steam_76500000000000000 5
        ```

    ??? info "/giveme_relic"
        **Syntax:** `/giveme_relic <Amount>`

        **Beschreibung:** Gibt dir selbst eine oder mehrere Lifmunk-Effigien.

        **Argumente:**

        - `<Amount>`: Anzahl der Lifmunk-Effigien.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /giveme_relic 5
        ```


    ??? info "/delitems"
        **Syntax:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **Beschreibung:** Entfernt mehrere Items in einem Befehl. Die Menge kann pro Item angegeben werden. Mit `all` werden alle Vorkommen gelöscht.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<ItemId>[:<Amount>] ...`: Liste von Items mit optionaler Mengenangabe.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **Syntax:** `/clearinv <UserId> [Container=items] ...`

        **Beschreibung:** Leert bestimmte Container aus dem Inventar eines Spielers. Verfügbare Container: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot` oder `all`.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `[Container] ...`: (Optional) Zu leerende Container. Standard: items.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "Pals"
    ??? info "/givepal"
        **Syntax:** `/givepal <UserId> <PalId> [Level=1]`

        **Beschreibung:** Gibt einem Spieler einen Pal auf dem angegebenen Level.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<PalId>`: Der zu vergebende Pal.
          **Hinweis:** Verwende den Entwickler-Namen des Pals, z. B. `WeaselDragon` (Chillet). Die vollständige Liste findest du unter [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Optional) Level des Pals. Standard: 1.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **Syntax:** `/givepal_j <UserID> <PalTemplate>`

        **Beschreibung:** Gibt einem Spieler einen Pal basierend auf einer PalTemplate-Datei. Eingebettetes JSON wird nicht mehr unterstützt; es wird ausschließlich ein Dateiname akzeptiert.

        **Hinweis:** Die `.json`-Dateiendung muss nicht angegeben werden; sie wird automatisch ergänzt, falls sie fehlt.

        **Argumente:**

        - `<UserID>`: Die ID des Spielers.
        - `<PalTemplate>`: Der Name der PalTemplate-Datei (siehe [PalTemplate](/FileTypes/PalTemplate)).

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **Syntax:** `/givemepal <PalId> [Level=1]`

        **Beschreibung:** Gibt dir selbst einen Pal auf dem angegebenen Level.

        **Argumente:**

        - `<PalId>`: Der Pal.
          **Hinweis:** Verwende den Entwickler-Namen des Pals, z. B. `WeaselDragon` (Chillet). Siehe [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Optional) Level des Pals. Standard: 1.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **Syntax:** `/givemepal_j <PalTemplate>`

        **Beschreibung:** Gibt dir selbst einen Pal basierend auf einer PalTemplate-Datei.

        **Argumente:**

        - `<PalTemplate>`: Der Name der PalTemplate-Datei (siehe [PalTemplate](/FileTypes/PalTemplate)).

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **Syntax:**
        Folgende Varianten sind möglich:

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **Beschreibung:** Spawnt einen Pal relativ zu dir oder an einer festen Position. **Bei RCON müssen x, y und z angegeben werden!**

        **Hinweis:** Alle Statuswerte außer dem Level werden zufällig generiert.

        **Argumente:**
        - `<PalID>`: Der zu spawnende Pal.
        - `[x]`: (Optional) X-Position. Standard: relativ zum Spieler.
        - `[y]`: (Optional) Y-Position. Standard: relativ zum Spieler.
        - `[z]`: (Optional) Z-Position. Standard: relativ zum Spieler.
        - `[Level]`: (Optional) Level des Pals. Standard: 1.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /spawnpal Anubis 255
        ```
        _Spawnt einen Anubis auf Level 255!_

    ??? info "/spawnpal_j"
        **Syntax:**
        Folgende Varianten sind möglich:

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal <PalTemplate> [x] [y] [z]`

        **Beschreibung:** Spawnt einen Pal relativ zu dir oder an einer festen Position. **Bei RCON müssen x, y und z angegeben werden!**

        **Hinweis:** Alle Statuswerte außer dem Level werden zufällig generiert.

        **Argumente:**

        - `<PalTemplate>`: Der Name der PalTemplate-Datei.
        - `[x]`: (Optional) X-Position. Standard: relativ zum Spieler.
        - `[y]`: (Optional) Y-Position. Standard: relativ zum Spieler.
        - `[z]`: (Optional) Z-Position. Standard: relativ zum Spieler.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /spawnpal Anubis 255
        ```
        _Spawnt einen Anubis auf Level 255!_

    ??? info "/summon"
        **Syntax:** `/summon <PalSummon>`

        **Beschreibung:** Spawnt einen Pal mithilfe einer PalSummon-Datei.

        **Hinweis:** Die `.json`-Dateiendung muss nicht angegeben werden; sie wird automatisch ergänzt, falls sie fehlt.

        **Argumente:**
        - `<PalSummon>`: Der Name der PalSummon-Datei.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **Syntax:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **Beschreibung:** Gibt einem Spieler ein Pal-Ei mit einem bestimmten Pal und optional angepasstem Level.

        **Argumente:**

        ??? quote "<UserId\>"
            **Beschreibung:** Die ID des Spielers.

        ??? quote "<EggId\>"
            **Beschreibung:** Der Typ des Eis (01 = klein, 05 = groß).

            **Note:** Erlaubte Werte sind von 01 (smallest) bis 05 (largest) für jeden Eityp:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **Beschreibung:** Der Pal im Ei.

            **Note:** Verwende das `AssetName` vom jeweiligen Pal, z.B. `WeaselDragon` für den Chillet. Eine komplette Liste aller Asset-Namen findest du auf [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level\]"
            **Beschreibung:** (Optional) Level des Pals im Ei.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **Syntax:** `/givemeegg <EggId> <PalId> [Level]`

        **Beschreibung:** Gibt dir selbst ein Pal-Ei mit einem bestimmten Pal und optional angepasstem Level.

        **Argumente:**

        ??? quote "<EggId\>"
            **Beschreibung:** Der Typ des Eis (01 = klein, 05 = groß).

            **Note:** Erlaubte Werte sind von 01 (smallest) bis 05 (largest) für jeden Eityp:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **Beschreibung:** Der Pal im Ei.

            **Note:** Verwende das `AssetName` vom jeweiligen Pal, z.B. `WeaselDragon` für den Chillet. Eine komplette Liste aller Asset-Namen findest du auf [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level\]"
            **Beschreibung:** (Optional) Level des Pals im Ei.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **Syntax:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **Beschreibung:** Gibt ein Pal-Ei mit einem Pal aus einer PalTemplate-Datei und optional angepasstem Level.

        **Argumente:**

        ??? quote "<EggId\>"
            **Beschreibung:** Der Typ des Eis.

            **Hinweis:** Erlaubte Werte sind von 01 (kleinstes) bis 05 (größtes) für jeden Eityp:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **Beschreibung:** Der Name der zu verwendenden PalTemplate-Datei.

            **Hinweis:** Die `.json`-Dateiendung muss nicht angegeben werden; sie wird automatisch ergänzt, falls sie fehlt. Siehe [PalTemplate](/FileTypes/PalTemplate).

        ??? quote "[Level]"
            **Beschreibung:** (Optional) Level des Pals im Ei.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **Syntax:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **Beschreibung:** Gibt dir selbst ein Pal-Ei mit einem Pal aus einer PalTemplate-Datei und optional angepasstem Level.

        **Argumente:**

        ??? quote "<EggId\>"
            **Beschreibung:** Der Typ des Eis.

            **Hinweis:** Erlaubte Werte sind von 01 (kleinstes) bis 05 (größtes) für jeden Eityp:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **Beschreibung:** Der Name der zu verwendenden PalTemplate-Datei.

            **Hinweis:** Die `.json`-Dateiendung muss nicht angegeben werden; sie wird automatisch ergänzt, falls sie fehlt. Siehe [PalTemplate](/FileTypes/PalTemplate).

        ??? quote "[Level]"
            **Beschreibung:** (Optional) Level des Pals im Ei.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **Syntax:** `/jetragon`

        **Beschreibung:** Gibt dir einen Admin-Jetragon-Pal (er ist schneller weg, als du schauen kannst).

        **Argumente:** Keine

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **Syntax:** `/catwaifu`

        **Beschreibung:** Gibt dir eine Admin-Cat-Waifu, die deine Charakterwerte verstärkt.

        **Argumente:** Keine

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **Syntax:** `/exportpals [UserId]`

        **Beschreibung:** Exportiert alle Pals eines Spielers als PalTemplate-Dateien nach
        `Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/`.

        **Argumente:**

        - `[UserId]`: (Optional) Die ID des Spielers, dessen Pals exportiert werden sollen. Wird kein Wert angegeben, werden deine eigenen Pals exportiert.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **Syntax:** `/deletepals <UserId> <PalFilter>`

        **Beschreibung:** Löscht Pals eines Spielers anhand erweiterter Filter.
        Mit dem Filter können mehrere Kriterien (z. B. Pal-ID, Level, Geschlecht, Passive Skills usw.) kombiniert werden.
        **Bitte vor dem Einsatz auf wichtigen Daten unbedingt in einer sicheren Umgebung testen.**

        **Argumente:**

        ??? quote "<UserId\>"
            **Beschreibung:** Die ID des Spielers, dessen Pals gelöscht werden sollen.

        ??? quote "<PalFilter\>"
            **Beschreibung:** Eine Kombination von Filter-Schlüsselwörtern zur Auswahl der zu löschenden Pals.

            **Hinweis:** Mehrere Filter können in einem einzigen Befehl kombiniert werden.

            Verfügbare Filter-Schlüsselwörter:

            - `ID`: PalID oder Liste von PalIDs (kommagetrennt)
            - `Nick`: String (Name des Pals)
            - `Gender`: `male` oder `female`
            - `Level`: Zahl, unterstützt `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank`: Zahl, unterstützt `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky`: `true` oder `false` (shiny)
            - `Passives`: PassiveSkill oder Liste von PassiveSkills (kommagetrennt)
            - `Limit`: Zahl (maximale Anzahl zu löschender Pals)

            **Beispiel-Filter:**

            - `ID Serpent,PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /deletepals 76567890987654321 ID Serpent,PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "Forschungsbaum"
    ??? info "/learntech"
        **Syntax:** `/learntech <UserId> <TechID>`

        **Beschreibung:** Lässt einen Spieler eine bestimmte Technologie erlernen. Mit `all` werden alle freigeschaltet.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<TechID>`: Die Technologie, die gelernt werden soll. Verwende `all` um alle freizuschalten.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **Syntax:** `/unlearntech <UserId> <TechID>`

        **Beschreibung:** Entfernt eine bestimmte Technologie. Mit `all` werden alle entfernt.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<TechID>`: Die Technologie, die entfern werden soll. Verwende `all` um alle zu entfernen.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /unlearntech steam_76500000000000000 Tech001
        /unlearntech gdk_25300000000000000 all
        ```

    ??? info "/givetechpoints"
        **Syntax:** `/givetechpoints <UserId> <Amount>`

        **Beschreibung:** Gibt einem Spieler eine bestimmte Anzahl an Technologiepunkten.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<Amount>`: Anzahl der zu vergebenden Technologiepunkte.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **Syntax:** `/givebosstechpoints <UserId> <Amount>`

        **Beschreibung:** Gibt einem Spieler eine bestimmte Anzahl an uralten Technologiepunkten.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<Amount>`: Anzahl der zu vergebenden uralten Technologiepunkte.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **Syntax:** `/givemetechpoints <Amount>`

        **Beschreibung:** Gibt dir selbst eine bestimmte Anzahl an Technologiepunkten.

        **Argumente:**

        - `<Amount>`: Anzahl der Technologiepunkte.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **Syntax:** `/givemebosstechpoints <Amount>`

        **Beschreibung:** Gibt dir selbst eine bestimmte Anzahl an uralten Technologiepunkten.

        **Argumente:**

        - `<Amount>`: Anzahl der uralten Technologiepunkte.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemebosstechpoints 5
        ```


??? note "Data Mining"
    ??? info "/gettechids"
        **Syntax:** `/gettechids`

        **Beschreibung:** Gibt eine Liste aller verfügbaren Technologie-IDs zurück. Bei Nutzung über RCON erfolgt die Ausgabe im JSON-Format.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **Syntax:** `/getskinids`

        **Beschreibung:** Gibt eine Liste aller verfügbaren Pal-Skin-IDs zurück. Bei Nutzung über RCON erfolgt die Ausgabe im JSON-Format.

        **Argumente:**

        - Keine

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /getskinids
        ```
