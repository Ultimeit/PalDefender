# PalDefender REST API

Dieser Abschnitt dokumentiert die integrierte PalDefender REST API (eine kleine HTTP-Schnittstelle, die für den **lokalen / vertrauenswürdigen** Einsatz gedacht ist).

- **Standard-Basis-URL:** `http://127.0.0.1:17993`
- **Authentifizierung:** Bearer-Token (bei allen Endpunkten erforderlich)
- **Versions-Endpunkt:** `/v1/pdapi/version`

> Sicherheitshinweis: Setze diesen Port **nicht** direkt dem öffentlichen Internet aus.
> Wenn du Remote-Zugriff benötigst, verwende einen Reverse Proxy und geeignete Zugriffskontrollen.

## Inhalt
- [Authentifizierung & Einrichtung](authentication.md)
- [Endpunkte](endpoints.md)
