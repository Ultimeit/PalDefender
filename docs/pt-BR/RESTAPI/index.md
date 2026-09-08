# PalDefender REST API

Esta seção documenta o PalDefender REST API integrado (uma pequena interface HTTP destinada ao uso **local/confiável**).

- **URL base padrão:** `http://127.0.0.1:17993`
- **Autenticação:** Token do portador (obrigatório em todos os endpoints)
- **Endpoint da versão:** `/v1/pdapi/version`

> Nota de segurança: **não** exponha esta porta diretamente à Internet pública. Se precisar de acesso remoto, use um proxy reverso e controles de acesso adequados.

## O que há aqui
- [Autenticação e configuração](authentication.md)
- [Pontos finais](Endpoints/index.md)
