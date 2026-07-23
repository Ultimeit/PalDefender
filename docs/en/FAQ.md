# FAQ

??? faq "I've accidentally banned myself/someone. How can I unban them?"

    Use `/unban <UserId>`{.var-command} for account bans and `/unbanip <IP>`{.var-command} for IP bans. PalDefender ban records are stored in `../Pal/Binaries/Win64/PalDefender/Banlist.json`. If you edit the file manually, stop the server first or reload configuration after editing.

??? faq "<span class='pd-badge pd-badge--deprecated'>Deprecated</span> Old IP-ban cleanup through Config.json"

    Older wiki versions told admins to remove IP bans from `../Pal/Binaries/Win64/PalDefender/Config.json`. That path is deprecated for ban records. Use `/unbanip <IP>`{.var-command} or edit `../Pal/Binaries/Win64/PalDefender/Banlist.json` instead.

??? faq "I added or changed a PalTemplate or PalSummon file but the command fails."

    - Make sure the file is valid JSON. Remove comments and trailing commas.
    - Templates belong in `../Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
    - Summons belong in `../Pal/Binaries/Win64/PalDefender/Pals/Summons/`.
    - Use the filename without path, for example `/summon ArenaBoss`{.var-command}.
    - For summon files, check that `PalTemplate`, `X`, `Y`, and `Z` are present.
    - For template files, check that `PalID` is present and uses a valid Pal ID.

??? faq "Which ID should I use for commands: UserId, PlayerUId, name, or SteamID?"

    Most admin commands expect the player's UserId, such as `steam_...` or `gdk_...`. Use `/iwantplayerlist`{.var-command} in-game to show IDs in the player list, or use REST/API tooling if you have it enabled.

??? faq "Why does RCON require coordinates or a UserId for commands that work without them in chat?"

    RCON has no in-game player character, so PalDefender cannot infer your position or target. For commands like `/getpos`{.var-command}, `/tp`{.var-command}, `/spawnpal`{.var-command}, and base-location commands, provide the target player or coordinates explicitly.

??? faq "The REST API returns 401 or 403. What should I check?"

    - **401**: Check the `Authorization: Bearer <token>` header and make sure the token file is not named `TokenExample.json`.
    - **403**: Check token permissions and make sure the server has finished starting.
    - After changing tokens, restart the server or reload the API/token setup according to your host workflow.

??? faq "I cannot login as an admin, it says that admin commands are whitelist protected."

    Make sure you have added your IP to `../Pal/Binaries/Win64/PalDefender/Config.json` like this:
    ```json
    "useAdminWhitelist": true,
    "adminIPs": [
        "127.0.0.1",
        "196.128.2.*",
        "123.222.111.122",
        "111.111.111.111",
    ],
    ```
    Alternatively, you can set `useAdminWhitelist` to `false` but that is not recommended, since cheaters are known to have some kind of exploit to obtain admin password.

??? faq "My server crashes on startup."

    - Ensure PalDefender is the only one mod running - delete all other mods and see if the problem persists.
    - Check if PalDefender is on the newest version.
    - Check out our [discord](https://discord.gg/paldefender) for any announcements.
    - Rename `PalDefender` directory in `../Pal/Binaries/Win64/` and restart the server.
    - In certain cases installing [VC++ redistributable](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) can help.

??? faq "I cannot see certain symbols properly in my server console."

    Please use Windows Terminal (or any alternative with proper unicode support) instead of default windows console.

??? faq "How can I report crashes?"

    Send following files in the [issue section](https://github.com/Ultimeit/PalDefender/issues):
    
    - `.../Pal/Saved/Crashes/<random numbers>/CrashContext.runtime-xml`
    - `.../Pal/Binaries/Win64/PalDefender/Logs/<recent logs>`

    Make sure to drop any information you could see or assume that might be the reason. Dont forget the PalDefender version! Any information can be valuable!
