# Authentifizierung & Einrichtung

## API aktivieren

1. Öffne: `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Setze `"Enabled"` auf `true`
3. Starte den Server neu.

Beim Start solltest du Logs ähnlich zu diesen sehen:
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:28][info] [RESTAPI] Loaded 1 Bearer token.
<...>
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Port

- **Standardport:** `17993`

**Nicht öffentlich zugänglich machen.**
Wenn du von außerhalb deines LANs / deiner Maschine auf die API zugreifen möchtest, setze einen **Reverse Proxy** davor (nginx / Caddy / Traefik) und terminiere TLS dort. Die eigentliche PalDefender REST API sollte weiterhin nur an `localhost` oder ein privates Interface gebunden sein.

## Tokens

- Starte den Server einmal, um ein Beispiel-Token generieren zu lassen.
- Jede `.json`-Datei im Verzeichnis `Win64/PalDefender/RESTAPI/Tokens/` wird als gültige Token-Datei behandelt.
  (**Einzige Ausnahme:** `TokenExample.json`)
- Erstelle **ein Token pro Person bzw. Dienst**. Tokens sind **Passwörter**.

Beispiel für eine Token-Datei:
```json
{
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"
}
```

## Headers
Sende das Token über den standardmäßigen Authorization-Header:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python-Beispiel
```py
import requests

base_url = "http://127.0.0.1:17993"
# Tu das nicht. Speichere Tokens niemals direkt im Code.
# Verwende z. B. .env-Dateien. Dies dient nur der Demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```