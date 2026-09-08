# Autenticação e configuração

## Ativando o API

1. Abrir: `Win64/PalDefender/RESTAPI/RESTConfig.json`
2. Definir `"Enabled"` como `true`
3. Reinicie o servidor.

Na inicialização, você deverá ver registros semelhantes a:
```
[16:42:28][info] [RESTAPI] Loaded 'RESTConfig.json'.
[16:42:31][info] [RESTAPI] Loaded 1 Bearer token.
[16:42:31][info] [RESTAPI] Running PalDefender RESTAPI on port 17993
```

## Porto

- **Porta padrão:** `17993`

**Não o exponha publicamente.** Se você quiser acessar a API de fora da sua LAN/máquina, coloque-a atrás de um **proxy reverso** (nginx/Caddy/Traefik) e encerre o TLS nele. Mantenha a API REST real do PalDefender vinculada ao host local ou a uma interface privada.

## Fichas

- Inicie o servidor uma vez para gerar um token de exemplo.
- Cada arquivo `.json` dentro de `Win64/PalDefender/RESTAPI/Tokens/` é tratado como um arquivo token válido. (A única exceção é o arquivo `TokenExample.json`!)
- Faça **um token por person/service**. Os tokens são senhas.

Arquivo de token de exemplo:

```json
{
  "Name": "AdminPanel",
  "Token": "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa",
  "Permissions": [
    "REST.*"
  ]
}
```

    `Permissions` pode ser um string ou um array de strings. Use permissões mais restritas para painéis públicos ou automação que não deveriam ter acesso total de administrador.

## Cabeçalhos
Envie o token através do cabeçalho de autorização padrão:
```
Authorization: Bearer DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa
```

Python exemplo
```py
import requests

base_url = "http://127.0.0.1:17993"
# do not do this. Never store the token in any code. use smth like .env! This is only for demonstration.
token = "DblJITQxmavSbIWyYIEwHiND2SkMsq1LGesgmlhgzNgu230TGRlNFoWp5cavqgoa"

headers = {"Authorization": f"Bearer {token}"}

r = requests.get(base_url + "/v1/pdapi/version", headers=headers, timeout=10)
print(r.status_code, r.text)
```
