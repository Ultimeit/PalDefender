# Recursos e status atual

Esta página resume as opções de recursos voltadas ao usuário em PalDefender 1.9.1. Para padrões exatos, consulte [`Config.json`](./FileTypes/Config.md).

## Proteção ativa

- As detecções de dano, resistência, munição e duplicação do acampamento base podem ser trocadas de forma independente.
- O Anti-Vacuum bloqueia tentativas suspeitas de coleta remota de itens comuns, ovos de Pal, relíquias e notas. Os administradores ignoram as verificações suportadas quando `allowAdminCheats` está ativado.
- Item inválido, Pal-stat, receita de bancada, Doutor Surgi, respawn de emergência e outras verificações de ação do servidor permanecem como parte da camada de validação central.
- `BannedCampWorker` impede que IDs de caracteres configurados sejam atribuídos a uma base.

O recurso legado controlado pelas chaves `antiDupe...` é compilado a partir da versão atual. O detector de duplicação do acampamento base mais recente é separado e controlado por `baseCampDupeDetectionEnabled`.

## Administração e eventos

- `/admingun` (`/agun`) concede a [Admin Gun](./Commands/index.md) protegida no jogo a um administrador ativo.
- `/setting` pode inspecionar ou alterar temporariamente as configurações Palworld ativas suportadas.
- `/findbases` fornece uma fila de revisão interativa para bases empty/inactive.
- PalSummons oferece suporte a nomes de encontros, controles AI/damage-meter, multiplicadores de estatísticas, captura condicional, resultados de classificação e recompensas configuráveis. Consulte [`PalSummon.json`](./FileTypes/PalSummon.md).
- Os destinos Discord são configurados em `PalWebhooks` e abrangem chat, comandos, mortes, joins/leaves, convocações, eventos de plataformas petrolíferas e detecções anti-cheat.

## Batimento cardíaco

As compilações de lançamento enviam uma pulsação para `https://pallink.net/api/heartbeat` a cada 10 segundos após o jogo estar pronto. Sua carga útil contém world/server GUID, código de país de localidade do sistema operacional, versões PalDefender e Palworld, plataforma Windows/Wine/Proton, tempo de atividade do processo e online/maximum/unique-total contagens de jogadores. Não inclui nomes de jogadores, IDs de contas de jogadores, endereços IP de jogadores, mensagens de bate-papo ou conteúdo salvo. Ele é excluído das compilações de depuração.

## REST API

O REST API autenticado oferece suporte a fluxos de trabalho de jogador, Pal, inventário, tecnologia, progressão, guilda, banimento, mensagens, recompensa e moderação. A versão 1.9.0 também adiciona [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) e [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md).
