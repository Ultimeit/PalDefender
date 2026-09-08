# POST /ReloadConfig



**Ponto final:** `POST /v1/pdapi/ReloadConfig`

**Autenticação:** Token do portador

**Permissão:** `REST.Reload.Config`

## Objetivo

Recarrega a configuração PalDefender sem exigir uma reinicialização completa do servidor.

## Parâmetros de caminho

Nenhum.

## Parâmetros de consulta

Nenhum.

## Solicitar corpo

Opcional vazio JSON object.

## Esquema de resposta

--8<-- "_snippets/restapi/schemas/reload-config.md"

## Respostas de erro

Os corpos de erro usam esta forma:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "Human-readable message",
        "Details": {}
    }
}
```

| HTTP | Código de erro | Quando isso acontece |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | O cabeçalho `Authorization` está ausente, malformado ou não corresponde a um token de portador configurado. |
| `403` | `MISSING_PERMISSION` | O token é válido, mas não inclui essa permissão de endpoint. |

## Exemplos

### Recarregar configuração

```http
POST /v1/pdapi/ReloadConfig
```

### Recarregar após alterações de token

```http
POST /v1/pdapi/ReloadConfig
```

## Cenários

- Aplique edições nos arquivos de configuração suportados.
- Recarregue após atualizar `Banlist.json`, importar regras ou outros arquivos PalDefender legíveis em tempo de execução.
- Se uma alteração não entrar em vigor após o recarregamento, reinicie o servidor durante uma janela de manutenção.
