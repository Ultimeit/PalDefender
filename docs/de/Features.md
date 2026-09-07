# Funktionen und aktueller Stand

Diese Seite fasst die benutzerrelevanten Funktionsschalter in PalDefender 1.9.0 zusammen. Die genauen Standardwerte findest du unter [`Config.json`](./FileTypes/Config.md).

## Aktive Schutzfunktionen

- Damage-, Stamina-, Ammo- und BaseCamp-Dupe-Erkennung können unabhängig voneinander aktiviert oder deaktiviert werden.
- Anti-Vacuum blockiert verdächtige Aufnahmeversuche aus der Ferne für normale Gegenstände, Pal-Eier, Relikte und Notizen. Administratoren umgehen unterstützte Prüfungen, wenn `allowAdminCheats` aktiviert ist.
- Prüfungen für ungültige Gegenstände, Pal-Werte, Werkbankrezepte, Doctor Surgi, Notfall-Respawn und weitere Serveraktionen bleiben Bestandteil der zentralen Validierung.
- `BannedCampWorker` verhindert, dass konfigurierte Character-IDs an einer Basis eingesetzt werden.

Die alte, durch die `antiDupe...`-Schlüssel gesteuerte Funktion ist im aktuellen öffentlichen 1.9.0-Build deaktiviert. Die neuere BaseCamp-Dupe-Erkennung ist davon unabhängig und wird über `baseCampDupeDetectionEnabled` gesteuert.

## Administration und Events

- `/admingun` (`/agun`) gibt einem aktiven Administrator die geschützte [Admin-Waffe](./Commands/index.md).
- `/setting` kann unterstützte Palworld-Live-Einstellungen anzeigen oder vorübergehend ändern.
- `/findbases` bietet eine interaktive Prüfliste für leere bzw. inaktive Basen.
- PalSummons unterstützen Begegnungsnamen, KI-/Schadensmesser-Steuerung, Statusmultiplikatoren, bedingtes Fangen, Ranglisten und konfigurierbare Belohnungen. Siehe [`PalSummon.json`](./FileTypes/PalSummon.md).
- Discord-Ziele werden unter `PalWebhooks` konfiguriert und unterstützen Chat, Befehle, Todesfälle, Verbindungen, Summons, Oil-Rig-Ereignisse und AntiCheat-Erkennungen.

## Heartbeat

Release-Builds senden nach dem Spielstart alle 10 Sekunden einen Heartbeat an `https://pallink.net/api/heartbeat`. Der Payload enthält World/Server-GUID, Ländercode der Betriebssystem-Locale, PalDefender- und Palworld-Version, Windows/Wine/Proton-Plattform, Prozesslaufzeit sowie Online-, Maximum- und Gesamtzahl eindeutiger Spieler. Spielernamen, Spieler-Account-IDs, Spieler-IP-Adressen, Chatnachrichten und Speicherinhalte sind nicht enthalten. Debug-Builds senden keinen Heartbeat.

## REST API

Die authentifizierte REST API unterstützt Spieler-, Pal-, Inventar-, Technologie-, Fortschritts-, Gilden-, Bann-, Nachrichten-, Belohnungs- und Moderationsabläufe. Version 1.9.0 ergänzt außerdem [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) und [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md).
