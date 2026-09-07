# Features and current status

This page summarizes the user-facing feature switches in PalDefender 1.9.0. For exact defaults, see [`Config.json`](./FileTypes/Config.md).

## Active protection

- Damage, stamina, ammunition, and base-camp duplication detections can be switched independently.
- Anti-Vacuum blocks suspicious remote pickup attempts for ordinary items, Pal eggs, relics, and notes. Administrators bypass supported checks when `allowAdminCheats` is enabled.
- Invalid item, Pal-stat, workbench-recipe, Doctor Surgi, emergency-respawn, and other server-action checks remain part of the central validation layer.
- `BannedCampWorker` blocks configured Character IDs from being assigned at a base.

The legacy feature controlled by the `antiDupe...` keys is compiled out of the current public 1.9.0 build. The newer base-camp duplication detector is separate and controlled by `baseCampDupeDetectionEnabled`.

## Administration and events

- `/admingun` (`/agun`) grants the protected in-game [Admin Gun](./Commands/index.md) to an active administrator.
- `/setting` can inspect or temporarily change supported live Palworld settings.
- `/findbases` provides an interactive review queue for empty/inactive bases.
- PalSummons support encounter names, AI/damage-meter controls, stat multipliers, conditional capture, rank results, and configurable rewards. See [`PalSummon.json`](./FileTypes/PalSummon.md).
- Discord destinations are configured under `PalWebhooks` and cover chat, commands, deaths, joins/leaves, summons, Oil Rig events, and anti-cheat detections.

## Heartbeat

Release builds send a heartbeat to `https://pallink.net/api/heartbeat` every 10 seconds after the game is ready. Its payload contains the world/server GUID, OS-locale country code, PalDefender and Palworld versions, Windows/Wine/Proton platform, process uptime, and online/maximum/unique-total player counts. It does not include player names, player account IDs, player IP addresses, chat messages, or save contents. It is excluded from debug builds.

## REST API

The authenticated REST API supports player, Pal, inventory, technology, progression, guild, ban, messaging, reward, and moderation workflows. Version 1.9.0 also adds [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) and [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md).
