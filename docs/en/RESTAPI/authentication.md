# Authentication & Setup

## Enabling the API

1. Open: `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Set `"Enabled"` to `true`
3. Restart the server.

On startup you should see logs similar to:
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:28][info] [RESTAPI] Loaded 1 Bearer token.
<...>
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Port

- **Default port:** `17993`

**Do not expose it publicly.** If you want to access the API from outside your LAN / machine, put it behind a **reverse proxy** (nginx / Caddy / Traefik) and terminate TLS there. Keep the actual PalDefender REST API bound to localhost or a private interface.

## Tokens

- Start the server once to generate an example token.
- Every `.json` file inside `Win64/PalDefender/RESTAPI/Tokens/` is treated as a valid token file. (Only exception is the file `TokenExample.json`!)
- Make **one token per person/service**. Tokens are passwords.

Example token file:

```json
{
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"
}
```

## Headers
Send the token via the standard Authorization header:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python example
```py
import requests

base_url = "http://127.0.0.1:17993"
# do not do this. Never store the token in any code. use smth like .env! This is only for demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```