# PalDefender REST API

Dieser Abschnitt dokumentiert die eingebaute PalDefender REST API, eine kleine HTTP-Schnittstelle für **lokale / vertrauenswürdige** Nutzung.

- **Standard-Basis-URL:** `http://127.0.0.1:17993`
- **Authentifizierung:** Bearer-Token (auf allen Endpunkten erforderlich)
- **Versions-Endpunkt:** `/v1/pdapi/version`

> Sicherheitshinweis: Gib diesen Port **nicht** direkt im oeffentlichen Internet frei. Wenn du Fernzugriff brauchst, nutze einen Reverse Proxy und passende Zugriffskontrollen.

## Inhalt
- [Authentifizierung & Einrichtung](authentication.md)
- [Endpunkte](Endpoints/index.md)
