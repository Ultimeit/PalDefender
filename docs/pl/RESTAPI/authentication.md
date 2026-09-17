# Uwierzytelnianie i konfiguracja

## Włączanie API

1. Otwórz: `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Ustaw `"Enabled"` na `true`.
3. Uruchom serwer ponownie.

Podczas uruchamiania zobaczysz podobne komunikaty. Poniżej przetłumaczono ich znaczenie; rzeczywiste logi serwera są w języku angielskim:
```
[16:42:28][info] [RESTAPI] Wczytano 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Wczytano 1 token Bearer.
[16:42:31][info] [RESTAPI] Uruchomiono RESTAPI PalDefender na porcie 17993
```

## Port

- **Domyślny port:** `17993`

**Nie udostępniaj go publicznie.** Jeśli chcesz korzystać z API spoza sieci lokalnej lub komputera, umieść przed nim **odwrotny serwer proxy** (nginx / Caddy / Traefik) i obsługuj TLS na tym serwerze. Samo REST API PalDefender powinno nasłuchiwać tylko na localhost lub prywatnym interfejsie.

## Tokeny

- Uruchom serwer raz, aby wygenerować przykładowy token.
- Każdy plik `.json` w `Win64/PalDefender/RESTAPI/Tokens/` jest traktowany jako plik tokena. Jedynym wyjątkiem jest `TokenExample.json`!
- Utwórz **osobny token dla każdej osoby lub usługi**. Traktuj tokeny jak hasła.

Przykładowy plik tokena:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

`Permissions` może być ciągiem znaków lub tablicą ciągów znaków. Publicznym panelom i automatyzacjom, które nie potrzebują pełnego dostępu administratora, przyznawaj tylko niezbędne uprawnienia.

## Nagłówki
Przekaż token w standardowym nagłówku Authorization:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Przykład w Pythonie
```py
import requests

base_url = "http://127.0.0.1:17993"
# To tylko przykład. Nie zapisuj prawdziwego tokena w kodzie. Użyj np. pliku .env!
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
