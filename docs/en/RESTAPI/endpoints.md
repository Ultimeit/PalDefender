# Endpoints

> **Auth:** Bearer token (all endpoints below)

> **Base path:** `/v1/pdapi`

> **Content-Type:** `application/json` (for POST requests)

??? info "GET `/v1/pdapi/version` — PD version check"
    ## GET `/v1/pdapi/version`
    ### What it does
    Returns the running PalDefender build/version information.

    This is the simplest **health + compatibility** endpoint:

    - If this responds, your REST API is reachable
    - your token works
    - the server is alive

    ### When to use it

    - Sanity-check REST setup (URL/port/token)
    - Detect server/plugin version in tooling (dashboards, admin panels, scripts)
    - Guard client behavior by version (e.g., only show features if supported)

    ### Returns
    PalDefender version object.

    ### Response (example)
    ```json
    {
        "major": 1,
        "minor": 7,
        "patch": 1,
        "build": 3323,
        "version_str": "1.7.1",
        "version_str_long": "1.7.1.3323"
    }
    ```

??? info "GET `/v1/pdapi/guilds` — List all guilds"
    ## GET `/v1/pdapi/guilds`
    ### What it does
    Returns a list/map of all known guilds on the server, keyed by guild ID.

    This is a **directory** endpoint: it gives identifiers + basic metadata you can use to query individual guilds.

    ### When to use it

    - Build a guild selector dropdown in an admin UI
    - Discover guild IDs so you can call `GET /v1/pdapi/guild/<guild_id>`
    - Perform audits across guilds (e.g., list all guild names and owners)

    !!! note
        Treat the response as a snapshot. Guild membership and metadata can change immediately after you fetch it.

    ### Returns
    All known guilds indexed by guild ID.

    ### Response (example)
    ```json
    {
        "EAF4C152-4B581B5E-4281D299-53459513": {
            "name": "Unnamed Guild",
            "Level": 3,
            "admin": {
                "id": "805C3C33-00000000-00000000-00000000",
                "name": "Zvendson"
            },
            "camp_count": 1,
            "camps": [
                {
                    "id": "584E52BB-40692783-01F26F82-590C53E0",
                    "world_pos": {
                        "x": -321654.0165656156,
                        "y": 214182.5577156711,
                        "z": -762.5510371185613
                    },
                    "map_pos": {
                        "x": 122.40208652651658,
                        "y": -430.86278118870507,
                        "z": -762.5510371185613
                    }
                }
            ],
            "member_count": 1,
            "members": [
                "805C3C33-00000000-00000000-00000000"
            ]
        },
        "E278B61B-4F7366DC-D60E258C-36848A81": {
            "name": "Unnamed Guild",
            "Level": 1,
            "admin": {
                "id": "966E5969-00000000-00000000-00000000",
                "name": "スベンド"
            },
            "camp_count": 0,
            "camps": [],
            "member_count": 1,
            "members": [
                "966E5969-00000000-00000000-00000000"
            ]
        }
    }
    ```

??? info "GET `/v1/pdapi/guild/<guild_id>` — Guild details"
    ## GET `/v1/pdapi/guild/<guild_id>`
    ### Path parameters

    - `guild_id` (string): The guild identifier, usually obtained from `GET /v1/pdapi/guilds`
      Example: `EAF4C152-4B581B5E-4281D299-53459513`

    ### What it does
    Returns full details for one guild.

    This is the **deep view**: members, camps/bases, and other guild-specific data your server exposes.

    ### When to use it

    - Display a guild detail page in admin tooling
    - Inspect members (names, online/offline status)
    - Inspect bases/camps and related guild structures

    ### Returns
    Detailed information for a single guild.

    ### Response (example)
    ```json
    {
        "name": "Unnamed Guild",
        "Level": 3,
        "admin": {
            "id": "805C3C33-00000000-00000000-00000000",
            "name": "Zvendson"
        },
        "member_count": 1,
        "members": [
            {
                "player_uid": "805C3C33-00000000-00000000-00000000",
                "player_name": "Zvendson",
                "status": "Logout"
            }
        ],
        "camp_count": 1,
        "camps": [
            {
                "id": "584E52BB-40692783-01F26F82-590C53E0",
                "level": 3,
                "world_pos": {
                    "x": -321654.0165656156,
                    "y": 214182.5577156711,
                    "z": -762.5510371185613
                },
                "map_pos": {
                    "x": 122.40208652651658,
                    "y": -430.86278118870507,
                    "z": -762.5510371185613
                },
                "state": "Normal",
                "pals": {
                    "EEB6DA46-4C66DBCE-7304C6B1-CBCACEA1": {
                        "nickname": "OPnubis",
                        "pal_id": "BOSS_Anubis",
                        "npc_id": "None",
                        "skin_id": "None",
                        "gender": "None",
                        "level": 100,
                        "shiny": true,
                        "phisical_health": "Severe",
                        "worker_sick": "DepressionSprain",
                        "san": 0.0,
                        "imported": false,
                        "friendship": 1005,
                        "active_skills": [
                            "DragonBreath",
                            "RockLance",
                            "Unique_Anubis_GroundPunch"
                        ],
                        "learnt_skills": [
                            "DragonBreath"
                        ],
                        "passives": []
                    }
                },
                "buildings": "WIP"
            }
        ],
        "items": {
            "container_id": "F3C7D8A4-496CFBD1-F7884E81-B5B50487",
            "current": 0,
            "max": 54,
            "0": {},
            "1": {},
            "2": {},
            "3": {},
            "4": {},
            "5": {},
            "6": {},
            "7": {},
            "8": {},
            "9": {},
            "10": {},
            "11": {},
            "12": {},
            "13": {},
            "14": {},
            "15": {},
            "16": {},
            "17": {},
            "18": {},
            "19": {},
            "20": {},
            "21": {},
            "22": {},
            "23": {},
            "24": {},
            "25": {},
            "26": {},
            "27": {},
            "28": {},
            "29": {},
            "30": {},
            "31": {},
            "32": {},
            "33": {},
            "34": {},
            "35": {},
            "36": {},
            "37": {},
            "38": {},
            "39": {},
            "40": {},
            "41": {},
            "42": {},
            "43": {},
            "44": {},
            "45": {},
            "46": {},
            "47": {},
            "48": {},
            "49": {},
            "50": {},
            "51": {},
            "52": {},
            "53": {}
        },
        "expeditions": {
            "finished": 0,
            "missions": {
                "DUNGEON_GRASS": false,
                "DUNGEON_FOREST": false,
                "DUNGEON_VOLCANO": false,
                "DUNGEON_DESERT": false,
                "DUNGEON_SNOW": false,
                "DUNGEON_SAKURAJIMA": false,
                "DUNGEON_DARKISLAND": false
            }
        },
        "laboratory": {
            "current_research": "None",
            "researches": {}
        }
    }
    ```

??? info "POST `/v1/pdapi/give` — Grant EXP / items / pals / eggs (atomic)"
    ## POST `/v1/pdapi/give`
    ### What it does
    Grants rewards to a target player in a single server-side transaction-like operation:

    - EXP and/or
    - items and/or
    - pals and/or
    - eggs
    depending on the request body.

    ### Core behavior
    This endpoint is intended to behave **atomically**:

    - either everything is granted
    - or nothing is granted

    If any part fails (invalid input, missing inventory space, invalid IDs, etc.), the server should reject the request and not partially apply it.

    ### Why this matters
    Admin tooling must not accidentally:

    - give EXP but not items
    - give some items but fail on later items
    - spawn pals without placing items

    Atomic behavior avoids messy states and “support tickets from hell”.

    ### What it can grant
    Depending on your implementation, the request may include:

    - `EXP` — adds experience
    - `Lifmunks` — adds Lifmunk Effigy points
    - `TechnologyPoints` — adds tech points
    - `AncientTechnologyPoints` — adds ancient tech points
    - `UnlockTechnology` / `Techs[]` — learn technologies
    - `Items[]` — give one or more items with counts
    - `Pals[]` — give pals by ID + level
    - `PalTemplates[]` — import pal templates by filename
    - `PalEggs[]` — eggs by ID + pal ID / template, optionally with level

    ### Validation & common failure cases
    Typical reasons admins hit errors:

    - Inventory space: not enough room for all items → fail the entire request
    - Invalid IDs: unknown `ItemID`, `PalID`, `EggID`, or missing template file → fail
    - Invalid values:
        - negative / zero counts (depending on rules)
        - invalid levels (too low/high, or non-numeric)
        - missing required fields (e.g., no `UserID`)
    - Player not found / not loaded:
        - user ID not known
        - player not currently online (depending on how your server handles offline grants)

    ### Returns
    Error count and error messages. If status is not 200, you can check "Errors" for how many errors occured. in "Error" will be a more detailed list of what has failed.

    ### Request body (example)
    ```json
    {
        "UserID": "steam_76561198033245345",
        "EXP": 100000,
        "Lifmunks": 500,
        "TechnologyPoints": 500,
        "AncientTechnologyPoints": 500,
        "UnlockTechnology": "All",
        "Items": [
            { "ItemID": "Launcher_Default_5", "Count": 1 },
            { "ItemID": "ExplosiveBullet", "Count": 500 },
            { "ItemID": "LaserGatlingGun_5", "Count": 1 },
            { "ItemID": "LaserGatlingBullet", "Count": 500 },
            { "ItemID": "MultiGuidedMissileLauncher_5", "Count": 1 },
            { "ItemID": "MissileBullet", "Count": 500 },
            { "ItemID": "EnergyRocketLauncher_5", "Count": 1 },
            { "ItemID": "EnergyLauncherBullet", "Count": 500 }
        ],
        "Pals": [
            { "PalID": "Anubis", "Level": 33 },
            { "PalID": "Kirin", "Level": 13 },
            { "PalID": "AmaterasuWolf", "Level": 19 },
            { "PalID": "WhiteTiger_Ground", "Level": 35 }
        ],
        "PalTemplates": [
            "OPnubis.json"
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Normal_01", "PalID": "Kirin", "Level": 15 },
            { "EggID": "PalEgg_Fire_01", "PalID": "Kirin" },
            { "EggID": "PalEgg_Electricity_01", "PalTemplate": "OPnubis.json", "Level": 15 },
            { "EggID": "PalEgg_Electricity_01", "PalTemplate": "OPnubis.json" }
        ]
    }
    ```

    ### Response (success example)
    Status: 200
    ```json
    {
        "Errors": 0,
        "Error": {}
    }
    ```

    ### Response (failure example)
    Status: 400
    ```json
    {
        "Errors": 3,
        "Error": {
            "PalTemplates": [
                "PalTemplate 1: Could not import \"OPnubis.json\". ImportError: File 'D:\\AnotherPalServer\\Pal\\Binaries\\Win64\\PalDefender\\Pals\\Templates\\OPnubis.json' does not exist."
            ],
            "PalEggs": [
                "PalEgg 3: Could not import PalTemplate \"OPnubis.json\". ImportError: File 'D:\\AnotherPalServer\\Pal\\Binaries\\Win64\\PalDefender\\Pals\\Templates\\OPnubis.json' does not exist.",
                "PalEgg 4: Could not import PalTemplate \"OPnubis.json\". ImportError: File 'D:\\AnotherPalServer\\Pal\\Binaries\\Win64\\PalDefender\\Pals\\Templates\\OPnubis.json' does not exist."
            ]
        }
    }
    ```
