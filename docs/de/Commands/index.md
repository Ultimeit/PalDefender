# Befehle

## Was sind Befehle?

Befehle sind spezielle textbasierte Anweisungen, mit denen du mit dem Spiel interagieren kannst. Wenn du Befehle in den Chat eingibst, kannst du Aktionen wie Teleportieren, Spawnen von Kreaturen oder Spielerverwaltung ausführen. Befehle beginnen normalerweise mit <span class="var-command">/</span>, gefolgt vom Befehlsnamen und optionalen Argumenten.

## Wer kann Befehle verwenden?

**Aktuell gibt es keinen Befehl, den Nicht-Admins verwenden können.**
In der aktuellen Version sind nur Admin- und RCON-Befehle verfügbar.

## Befehlsliste

!!! note "Befehlssyntax"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → Muss angegeben werden.<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → Kann weggelassen werden. <span class="var-command-optional">{?}</span> zeigt den Standardwert an, der dann verwendet wird.
    </p>
    <p>
    Argumente haben unterschiedliche Typen. Am häufigsten sind <span class="var-string">Strings</span>, <span class="var-number">Zahlen</span>, <span class="var-float">Floats</span> und <span class="var-bool">Booleans</span>. Manche Befehle haben auch komplexe Typen wie bestimmte <span class="file">Dateinamen</span> in einem speziellen Ordner oder einen <span class="var-filter">Filter</span>.
    </p>

!!! tip "ID-Suche"
    Nutze [paldeck.cc/pals](https://paldeck.cc/pals) für `PalID`, [paldeck.cc/items](https://paldeck.cc/items) für `ItemID`, [paldeck.cc/technology](https://paldeck.cc/technology) für `TechID`, [paldeck.cc/buildings](https://paldeck.cc/buildings) für `BuildingID`, [paldeck.cc/passives](https://paldeck.cc/passives) für `PassiveID` und [paldeck.cc/skills](https://paldeck.cc/skills) für Skill-IDs.

??? note "Nur RCON"
    ??? info "/getrconcmds"
        **Syntax:** `/getrconcmds`

        **Beschreibung:** Gibt eine Liste aller per RCON nutzbaren Befehle inklusive benötigter Argumentanzahl zurück.

        **Argumente:**

        - None

        **Berechtigungen:** `RCON`

        **Beispiel:**
        ```
        /getrconcmds
        ```

??? note "Server Management"
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

??? note "Base Management"
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


??? note "Player Management"
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

??? note "Player Character"
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

??? note "Guild Management"
    ??? info "/setguildleader"
        **Syntax:** `/setguildleader <UserId>`

        **Beschreibung:** Macht den Zielspieler zum Leiter seiner aktuellen Gilde.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers, der Gildenleiter werden soll.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **Syntax:** `/exportguilds`

        **Beschreibung:** Exportiert alle Gilden des Servers nach Pal/Binaries/Win64/PalDefender/guildexport.json.

        **Argumente:**

        - None

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /exportguilds
        ```
        Beispiel-Ausgabedatei: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "Items"
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


??? note "Pals"
    ??? info "/givepal"
        **Syntax:** `/givepal <UserId> <PalId> [Level=1]`

        **Beschreibung:** Gibt einem Spieler einen Pal auf dem angegebenen Level.

        **Argumente:**

        - `<UserId>`: Die ID des Spielers.
        - `<PalId>`: Der zu gebende Pal.
            - **Note:** Nutze die Pal-ID, z. B. `WeaselDragon` (Chillet). Die vollständige Liste findest du auf [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Optional) Level des Pals. Standard: 1.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **Syntax:** `/givepal_j <UserID> <PalTemplate>`

        **Beschreibung:** Gibt einem Spieler einen Pal aus einer PalTemplate-Datei. Eingebettetes JSON wird nicht mehr unterstützt; es wird nur ein Dateiname akzeptiert.

        **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

        **Argumente:**

        - `<UserID>`: Die ID des Spielers.
        - `<PalTemplate>`: Der Name der PalTemplate-Datei (siehe [PalTemplate](../FileTypes/PalTemplate.md)).

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **Syntax:** `/givemepal <PalId> [Level=1]`

        **Beschreibung:** Gibt dir selbst einen Pal auf dem angegebenen Level.

        **Argumente:**

        - `<PalId>`: Der Pal, den du dir selbst gibst.
            - **Note:** Nutze die Pal-ID, z. B. `WeaselDragon` (Chillet). Die vollständige Liste findest du auf [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Optional) Level des Pals. Standard: 1.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **Syntax:** `/givemepal_j <PalTemplate>`

        **Beschreibung:** Gibt dir selbst einen Pal aus einer PalTemplate-Datei. Eingebettetes JSON wird nicht mehr unterstützt; es wird nur ein Dateiname akzeptiert.

        **Argumente:**

        - `<PalTemplate>`: Der Name der PalTemplate-Datei (siehe [PalTemplate](../FileTypes/PalTemplate.md)).

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **Syntax:**
        Any of the following works:

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **Beschreibung:** Spawnt einen Pal relativ oder absolut zu dir. **RCON muss x, y und z angeben!**

        **Note:** All stats, except level, are randomized.

        **Argumente:**
        - `<PalID>`: Der zu spawnende Pal.
        - `[x]`: (Optional) X-Position des Pals. Standard: Relativ zum aufrufenden Spieler.
        - `[y]`: (Optional) Y-Position des Pals. Standard: Relativ zum aufrufenden Spieler.
        - `[z]`: (Optional) Z-Position des Pals. Standard: Relativ zum aufrufenden Spieler.
        - `[Level]`: (Optional) Level des Pals. Standard: 1.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /spawnpal Anubis 255
        ```
        _Spawns an Anubis with level 255!_

    ??? info "/spawnpal_j"
        **Syntax:**

        Any of the following works:

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal <PalTemplate> [x] [y] [z]`

        **Beschreibung:** Spawnt einen Pal relativ oder absolut zu dir. **RCON muss x, y und z angeben!**

        **Note:** All stats, except level, are randomized.

        **Argumente:**

        - `<PalTemplate>`: Der Name der zu verwendenden PalTemplate-Datei.
        - `[x]`: (Optional) X-Position des Pals. Standard: Relativ zum aufrufenden Spieler.
        - `[y]`: (Optional) Y-Position des Pals. Standard: Relativ zum aufrufenden Spieler.
        - `[z]`: (Optional) Z-Position des Pals. Standard: Relativ zum aufrufenden Spieler.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /spawnpal Anubis 255
        ```
        _Spawns an Anubis with level 255!_

    ??? info "/summon"
        **Syntax:** `/summon <PalSummon>`

        **Beschreibung:** Spawnt einen Pal anhand der angegebenen PalSummon-Datei.

        **Note:** You do not need to include the .json extension in the filename; the system will append it automatically if missing.

        **Argumente:**
        - `<PalSummon>`: Der Name der zu verwendenden PalSummon-Datei.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **Syntax:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **Beschreibung:** Gibt dem Zielbenutzer ein Pal-Ei mit einem bestimmten Pal und optional angepasstem Level.

        **Argumente:**

        ??? quote "<UserId\>"
            **Beschreibung:** Die ID des Spielers, der das Ei erhalten soll.

        ??? quote "<EggId\>"
            **Beschreibung:** Der Typ des zu gebenden Eis.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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
            **Beschreibung:** Der Pal, der im Ei enthalten sein wird.

            **Note:** Nutze die Pal-ID, z. B. `WeaselDragon` (Chillet). Die vollständige Liste findest du auf [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level\]"
            **Beschreibung:** (Optional) Das Level des Pals im Ei.

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
            **Beschreibung:** Der Typ des Eis, das du dir selbst gibst.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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
            **Beschreibung:** Der Pal, der im Ei enthalten sein wird.

            **Note:** Nutze die Pal-ID, z. B. `WeaselDragon` (Chillet). Die vollständige Liste findest du auf [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level]"
            **Beschreibung:** (Optional) Das Level des Pals im Ei.

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
            **Beschreibung:** Der Typ des zu gebenden Eis.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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

            **Hinweis:** Du musst die Dateiendung .json nicht im Dateinamen angeben; das System hängt sie automatisch an, wenn sie fehlt. Siehe [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Level]"
            **Beschreibung:** (Optional) Das Level des Pals im Ei.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **Syntax:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **Beschreibung:** Gibt dir selbst ein Pal-Ei mit einem Pal aus einer PalTemplate-Datei und optional angepasstem Level.

        **Argumente:**

        ??? quote "<EggI\>"
            **Beschreibung:** Der Typ des Eis, das du dir selbst gibst.

            **Note:** Allowed values are from 01 (smallest) to 05 (largest) for each type:

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

            **Hinweis:** Du musst die Dateiendung .json nicht im Dateinamen angeben; das System hängt sie automatisch an, wenn sie fehlt. Siehe [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Level]"
            **Beschreibung:** (Optional) Das Level des Pals im Ei.

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **Syntax:** `/jetragon`

        **Beschreibung:** Gibt dir einen Admin-Jetragon-Pal (er ist seeehr... schnell weg).

        **Argumente:**
        - None

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **Syntax:** `/catwaifu`

        **Beschreibung:** Gibt dir eine Admin-Cat-Waifu, die deine Charakterwerte verstärkt.

        **Argumente:**

        - None

        **Berechtigungen:** `Chat`, `Admin`

        **Beispiel:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **Syntax:** `/exportpals [UserId]`

        **Beschreibung:** Exportiert jeden Pal eines Spielers als PalTemplate-Datei nach Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/.

        **Argumente:**

        - `[UserId]`: (Optional) Die ID des Spielers, dessen Pals exportiert werden. Wenn weggelassen, werden deine eigenen Pals exportiert.

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **Syntax:** `/deletepals <UserId> <PalFilter>`

        **Beschreibung:** Löscht Pals eines angegebenen Benutzers mit erweiterten Filtern. Der Filter erlaubt mehrere Kriterien wie Pal-ID, Level, Geschlecht, Passives usw. in einem Befehl. Bitte zuerst in einer sicheren Umgebung testen.

        **Argumente:**

        ??? quote "<UserId\>"
            **Beschreibung:** Die ID des Spielers, dessen Pals gelöscht werden.

        ??? quote "<PalFilter\>"
            **Beschreibung:** Eine Gruppe von Filter-Schlüsselwörtern zur Auswahl der zu löschenden Pals.

            **Note:** Multiple keywords can be combined in one command.

            Available filter keywords:

            - `ID`: PalID or list of PalIDs (comma-separated)
            - `Nick`: String (name of the Pal)
            - `Gender`: `male` or `female`
            - `Level`: Number, supports symbols `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank`: Number, supports symbols `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky`: `true` or `false` (shiny)
            - `Passives`: PassiveSkill or list of PassiveSkills (comma-separated)
            - `Limit`: Number (max number of Pals to delete)

            **Beispielfilter:**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            For more details, see the [PalFilter documentation](https://github.com/Ultimeit/PalDefender/blob/master/Wiki/Commands/deletepals.md).

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "Research Tree"
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


??? note "Data mining"
    ??? info "/gettechids"
        **Syntax:** `/gettechids`

        **Beschreibung:** Gibt eine Liste aller verfügbaren Technologie-IDs zurück. RCON erhält JSON-Ausgabe.

        **Argumente:**

        - None

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **Syntax:** `/getskinids`

        **Beschreibung:** Gibt eine Liste aller verfügbaren Pal-Skin-IDs zurück. RCON erhält JSON-Ausgabe.

        **Argumente:**

        - None

        **Berechtigungen:** `Chat`, `RCON`, `Admin`

        **Beispiel:**
        ```
        /getskinids
        ```
