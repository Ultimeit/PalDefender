# Authentifizierung & Einrichtung

## API aktivieren

1. Öffne: `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Setze `"Enabled"` auf `true`
3. Starte den Server neu.

Beim Start solltest du aehnliche Logs sehen:
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Loaded 1 Bearer token.
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Port

- **Standard-Port:** `17993`

**Nicht öffentlich freigeben.** Wenn du von außerhalb deines LANs oder Rechners auf die API zugreifen willst, setze sie hinter einen **Reverse Proxy** (nginx / Caddy / Traefik) und beende TLS dort. Binde die eigentliche PalDefender REST API an localhost oder ein privates Interface.

## Tokens

- Starte den Server einmal, um ein Beispiel-Token zu erzeugen.
- Jede `.json`-Datei in `Win64/PalDefender/RESTAPI/Tokens/` wird als gültige Token-Datei behandelt. (Einzige Ausnahme ist `TokenExample.json`!)
- Erstelle **ein Token pro Person/Dienst**. Tokens sind Passwoerter.

Beispiel-Token-Datei:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

    `Permissions` kann ein String oder ein Array von Strings sein. Nutze engere Berechtigungen für öffentliche Dashboards oder Automatisierungen, die keinen vollen Adminzugriff benötigen.

## Headers
Sende das Token über den Standard-Authorization-Header:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python-Beispiel
```py
import requests

base_url = "http://127.0.0.1:17993"
# Nicht so machen. Speichere echte Tokens nie im Code. Nutze z. B. .env! Das ist nur eine Demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
