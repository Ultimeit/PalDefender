# Pals

## /givepal { .toc-only }
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

## /givepal_j { .toc-only }
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

## /givemepal { .toc-only }
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

## /givemepal_j { .toc-only }
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

## /spawnpal { .toc-only }
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

## /spawnpal_j { .toc-only }
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

## /summon { .toc-only }
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

## /giveegg { .toc-only }
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


## /givemeegg { .toc-only }
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

## /giveegg_j { .toc-only }
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

## /givemeegg_j { .toc-only }
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

## /jetragon { .toc-only }
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

## /catwaifu { .toc-only }
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

## /exportpals { .toc-only }
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

## /deletepals { .toc-only }
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







