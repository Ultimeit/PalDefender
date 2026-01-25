# Endpunkte

> **Auth:** Bearer-Token (für alle unten aufgeführten Endpunkte erforderlich)

> **Basispfad:** `/v1/pdapi`

> **Content-Type:** `application/json` (für POST-Anfragen)

??? info "GET `/v1/pdapi/version` — PD-Versionsprüfung"
    ## GET `/v1/pdapi/version`
    ### Was dieser Endpunkt tut
    Gibt die aktuell laufende PalDefender-Build-/Versionsinformation zurück.

    Dies ist der einfachste **Health- + Kompatibilitäts-Endpunkt**:

    - Wenn dieser Endpunkt antwortet, ist die REST API erreichbar
    - dein Token ist gültig
    - der Server läuft

    ### Wann verwenden

    - Prüfung der REST-Einrichtung (URL/Port/Token)
    - Erkennung der Server-/Plugin-Version in Tools (Dashboards, Admin-Panels, Skripte)
    - Absicherung von Client-Verhalten per Versionsprüfung (z. B. Features nur anzeigen, wenn unterstützt)

    ### Rückgabe
    PalDefender-Versionsobjekt.

    ### Response (Beispiel)
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

??? info "GET `/v1/pdapi/guilds` — Alle Gilden auflisten"
    ## GET `/v1/pdapi/guilds`
    ### Was dieser Endpunkt tut
    Gibt eine Liste/Map aller bekannten Gilden auf dem Server zurück, indiziert nach Gilden-ID.

    Dies ist ein **Verzeichnis-Endpunkt**: Er liefert Identifikatoren und Basis-Metadaten, mit denen einzelne Gilden weiter abgefragt werden können.

    ### Wann verwenden

    - Aufbau einer Gilden-Auswahl in einem Admin-Interface
    - Ermitteln von Gilden-IDs für `GET /v1/pdapi/guild/<guild_id>`
    - Audits über alle Gilden hinweg (z. B. Namen und Anführer prüfen)

    !!! note
        Die Antwort ist als Momentaufnahme zu verstehen. Gildenmitgliedschaften und Metadaten können sich unmittelbar nach dem Abruf ändern.

    ### Rückgabe
    Alle bekannten Gilden, indexiert nach Gilden-ID.

    ### Response (Beispiel)
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

??? info "GET `/v1/pdapi/guild/<guild_id>` — Gildendetails"
    ## GET `/v1/pdapi/guild/<guild_id>`
    ### Pfadparameter

    - `guild_id` (string): Die Gilden-ID, üblicherweise aus `GET /v1/pdapi/guilds`
      Beispiel: `EAF4C152-4B581B5E-4281D299-53459513`

    ### Was dieser Endpunkt tut
    Gibt vollständige Details zu einer einzelnen Gilde zurück.

    Dies ist die **Detailansicht**: Mitglieder, Basen/Camps und weitere gildenbezogene Daten.

    ### Wann verwenden

    - Anzeige einer Gilden-Detailseite in Admin-Tools
    - Prüfung von Mitgliedern (Name, Online-/Offline-Status)
    - Analyse von Basen/Camps und gildenrelevanten Strukturen

    ### Rückgabe
    Detaillierte Informationen zu einer einzelnen Gilde.

    ### Response (Beispiel)
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

??? info "POST `/v1/pdapi/give` — EXP / Items / Pals / Eier vergeben (atomar)"
    ## POST `/v1/pdapi/give`
    ### Was dieser Endpunkt tut
    Vergibt Belohnungen an einen Zielspieler in einer einzigen serverseitigen, transaktionsähnlichen Operation:

    - EXP und/oder
    - Items und/oder
    - Pals und/oder
    - Eier

    abhängig vom Request-Body.

    ### Kernverhalten
    Dieser Endpunkt ist **atomar** ausgelegt:

    - entweder wird alles vergeben
    - oder es wird nichts vergeben

    Schlägt ein Teil fehl (ungültige Eingaben, fehlender Inventarplatz, ungültige IDs usw.), wird die Anfrage vollständig abgelehnt und es erfolgt keine Teilvergabe.

    ### Warum das wichtig ist
    Admin-Tools dürfen nicht versehentlich:

    - EXP vergeben, aber keine Items
    - nur einen Teil der Items vergeben
    - Pals spawnen, ohne begleitende Items zu platzieren

    Das atomare Verhalten verhindert inkonsistente Zustände und spätere Support-Probleme.

    ### Was vergeben werden kann
    Abhängig von der Implementierung kann die Anfrage enthalten:

    - `EXP` — Erfahrungspunkte
    - `Lifmunks` — Lifmunk-Effigien-Punkte
    - `TechnologyPoints` — Technologiepunkte
    - `AncientTechnologyPoints` — Uralte Technologiepunkte
    - `UnlockTechnology` / `Techs[]` — Technologien freischalten
    - `Items[]` — Items mit Mengenangaben
    - `Pals[]` — Pals per ID + Level
    - `PalTemplates[]` — PalTemplates per Dateiname importieren
    - `PalEggs[]` — Eier per ID + PalID / Template, optional mit Level

    ### Validierung & häufige Fehlerursachen
    Typische Fehlerquellen:

    - Inventarplatz: nicht genug Platz → gesamte Anfrage schlägt fehl
    - Ungültige IDs: unbekannte `ItemID`, `PalID`, `EggID` oder fehlende Template-Datei
    - Ungültige Werte:
        - negative / null Werte
        - ungültige Level
        - fehlende Pflichtfelder (z. B. `UserID`)
    - Spieler nicht gefunden / nicht geladen:
        - UserID unbekannt
        - Spieler nicht online (abhängig von der Serverlogik)

    ### Rückgabe
    Anzahl der Fehler und detaillierte Fehlermeldungen.
    Ist der Status ungleich 200, enthält `Errors` die Anzahl der Fehler und `Error` eine detaillierte Liste.

    ### Request-Body (Beispiel)
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

    ### Response (Erfolg)
    Status: 200
    ```json
    {
        "Errors": 0,
        "Error": {}
    }
    ```

    ### Response (Fehler)
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
