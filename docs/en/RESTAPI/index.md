# PalDefender REST API

This section documents the built-in PalDefender REST API (a small HTTP interface meant for **local / trusted** use).

- **Default base URL:** `http://127.0.0.1:17993`
- **Auth:** Bearer token (required on all endpoints)
- **Version endpoint:** `/v1/pdapi/version`

> Security note: do **not** expose this port directly to the public internet. If you need remote access, use a reverse proxy and proper access controls.

## What’s in here
- [Authentication & setup](authentication.md)
- [Endpoints](endpoints.md)
