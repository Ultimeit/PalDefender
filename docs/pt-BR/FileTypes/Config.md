# 🛠️ `Config.json`

`Config.json` é gerado em `<PalServer>/Pal/Binaries/Win64/PalDefender/` na primeira inicialização. Pare o servidor antes de editá-lo ou use `/reloadcfg` após salvar as alterações.

!!! note "Configurações geradas"
    PalDefender grava a configuração atual definida de volta neste arquivo. As chaves não listadas abaixo são obsoletas, apenas para migração ou não estão disponíveis na versão pública atual.

## Geral e aplicação

| Chave | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `version` | string | Versão atual | Marcador de configuração schema/version mantido por PalDefender. |
| `MOTD` | array | Três mensagens | Junte-se às mensagens. Suporta `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}` e `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | bool | `true` | Interrompe o servidor se PalDefender não puder inicializar. Alguns hosts podem interpretar isso como uma falha e reiniciar repetidamente. |
| `preventAdminPasswordInChat` | bool | `true` | Impede que a senha do administrador seja enviada como texto de bate-papo. |
| `shouldWarnCheaters` | bool | `true` | Avisa um jogador quando uma detecção automática é acionada. |
| `shouldWarnCheatersReason` | bool | `false` | Inclui o motivo da detecção nesse aviso. |
| `shouldKickCheaters` | bool | `true` | Expulsa trapaceiros detectados, a menos que uma ação habilitada mais forte seja aplicada. |
| `shouldBanCheaters` | bool | `false` | Banimentos de contas detectaram trapaceiros. |
| `shouldIPBanCheaters` | bool | `false` | Banimentos de IP detectaram trapaceiros. |
| `blockEmergencyRespawn` | bool | `true` | Bloqueia a ação Menu → Respawn de Emergência. |

## RCON e registro

| Chave | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` | Segundos antes de uma conexão RCON inativa expirar. |
| `RCONbase64` | bool | `false` | Ativa comandos RCON codificados em base64. |
| `logNetworking` | bool | `false` | Grava o log de rede compatível. O log de rede está desabilitado na versão pública atual. |
| `logNetworkingToConsole` | bool | `true` | Espelha o log de rede no console quando o log de rede está disponível. |
| `logChat` | bool | `true` | Registra bate-papo Global, Guild e Say. |
| `logRCON` | bool | `false` | Registra comandos RCON. |
| `logPlayerUID` | bool | `false` | Inclui PlayerUID em logs relevantes e webhooks anti-cheat. |
| `logPlayerIP` | bool | `true` | Inclui endereços IP em logs relevantes e webhooks anti-cheat. |
| `logPlayerDeaths` | bool | `true` | Registra mortes e mortes de jogadores. |
| `logPlayerLogins` | bool | `true` | Registra o jogador entrando e saindo. |
| `logPlayerBuildings` | bool | `true` | Os registros suportam atividades de construção, cancelamento, desmontagem e movimentação de Palbox. |
| `logPlayerSummons` | bool | `true` | Registra convocações de chefes de ataque de jogadores. |
| `logPlayerCaptures` | bool | `true` | Configuração de compatibilidade reservada. O log de captura está desabilitado na versão 1.9.0 porque o evento disponível não é confiável. |
| `logPlayerDamage` | bool | `false` | Registra eventos de dano originados pelo jogador e seus valores de dano native/base relatados no console do servidor. Funciona independentemente da detecção de fraudes de danos. |
| `BannedCampWorker` | array | Variantes do Panthalus | IDs de caracteres que não podem ser atribuídos em uma base. A correspondência não diferencia maiúsculas de minúsculas; variantes como `BOSS_...` devem ser listadas separadamente. |
| `logHelicopterKills` | bool | `true` | Registra mortes de helicópteros de combate. |
| `logCraftings` | bool | `true` | Registra a criação do jogador. |
| `logTechUnlocks` | bool | `true` | A tecnologia de registros é desbloqueada. |
| `logOpenOilrigBoxes` | bool | `true` | Registra eventos da caixa de meta final da plataforma petrolífera. |
| `OilrigGoalBoxLocktime` | interno | `300` | Segundos, a caixa de meta final da plataforma petrolífera permanece bloqueada. |

## Discord webhooks

`PalWebhooks` é um object. Deixe um URL individual vazio para desativar esse destino. A entrega do webhook está na fila, portanto, os bursts são escalonados em vez de bloquear o thread do jogo.

| Chave aninhada | Envia |
| --- | --- |
| `webhookURL_Chat` | Mensagens de bate-papo globais e Say. |
| `webhookURL_GuildChat` | Mensagens de bate-papo da guilda com o nome da guilda. |
| `webhookURL_Commands` | Os comandos são executados no chat do jogo, incluindo o administrador e o comando completo. |
| `webhookURL_Deaths` | Mortes e mortes. Requer `announcePlayerDeaths` ou `logPlayerDeaths`. |
| `webhookURL_JoinLeave` | Eventos Join/leave quando `announceConnections` está ativado; respeita `dontAnnounceAdminConnections`. |
| `webhookURL_Summons` | Player/admin anúncios de convocação e resultados completos de danos de convocação rastreada. |
| `webhookURL_Oilrig` | Caixas de plataformas petrolíferas e helicópteros matam quando a configuração `announce...` correspondente está habilitada. |
| `webhookURL_AntiCheats` | Detecções anti-cheat de revisão automática e manual. A inclusão de UID/IP segue `logPlayerUID` e `logPlayerIP`. |

```json
"PalWebhooks": {
    "webhookURL_Chat": "",
    "webhookURL_GuildChat": "",
    "webhookURL_Commands": "",
    "webhookURL_Deaths": "",
    "webhookURL_JoinLeave": "",
    "webhookURL_Summons": "",
    "webhookURL_Oilrig": "",
    "webhookURL_AntiCheats": ""
}
```

## Administração, bate-papo e anúncios

| Chave | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` | Restringe o administrador login/commands a `adminIPs`. |
| `adminAutoLogin` | bool | `false` | Ativa automaticamente o modo de administrador para um IP incluído na lista de permissões. |
| `adminIPs` | array | `127.0.0.1` | IPs exatos e entradas curinga suportadas permitidas para administrar o servidor. |
| `bannedChatWords` | array | Termos comuns do RMT | Termos de filtro de bate-papo que não diferenciam maiúsculas de minúsculas. |
| `bannedNames` | array | Nomes de abuso conhecidos | Nomes de jogadores rejeitados durante o login. |
| `allowAdminCheats` | bool | `false` | Permite que os administradores usem comandos em `adminCheats` e ignorem as proteções selecionadas. O próprio Admin Gun requer apenas status de administrador ativo no jogo. |
| `allowGodmodeOnehit` | bool | `false` | Permite que os usuários do Godmode causem dano de um golpe. |
| `adminCheats` | array | Lista gerada | Comandos tratados como truques administrativos quando `allowAdminCheats` está desativado. RCON não está bloqueado nesta lista. |
| `announceConnections` | bool | `false` | Anuncia joins/leaves no chat e ativa a origem do webhook join/leave. |
| `dontAnnounceAdminConnections` | bool | `true` | Oculta o administrador joins/leaves desses anúncios. |
| `announcePunishments` | bool | `false` | Anuncia cheat automático kicks/bans. |
| `announcePlayerDeaths` | bool | `false` | Anuncia mortes de jogadores no chat. |
| `announceOpenOilrigBoxes` | bool | `false` | Anuncia eventos de caixa de plataforma petrolífera e ativa sua fonte de webhook. |
| `announceHelicopterKills` | bool | `false` | Anuncia mortes de helicópteros e ativa sua fonte de webhook. |
| `announcePlayerSummons` | bool | `false` | Anuncia a convocação do chefe de ataque do jogador. |
| `announceAdminSummons` | bool | `false` | Anuncia Pals gerados por meio de recursos de convocação administrativa. |
| `announceAdminSummonsKill` | bool | `true` | Anuncia kills/deaths de Pals convocados administrativamente. |
| `chatBypassWait` | bool | `true` | Remove a espera normal do chat entre mensagens. |
| `chatMessageMaxLen` | interno | `128` | Duração máxima aceita da mensagem de bate-papo. |
| `useWhitelist` | bool | `false` | Ativa `WhiteList.json`. |
| `whitelistMessage` | string | Texto gerado | Mensagem mostrada a um jogador rejeitado que não está na lista de permissões. |
| `steamidProtection` | bool | `true` | Rejeita o uso simultâneo duplicado de um UserId. |

## Validação de jogabilidade

| Chave | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | interno | `100` | Danos máximos permitidos de PvP a edifícios. |
| `pvpMaxToPalDamage` | interno | `1000` | Dano máximo permitido de PvP a Pals. |
| `pveMaxToPalBanThreshold` | interno | `900000` | PvE Limite de dano ao Pal usado pela detecção de cheats. |
| `droppedPalPickupRange` | interno | `99999` | Distância máxima aceita para uma coleta de Pal perdido. |
| `treeLimiter` | float | `0.1` | Segundos mínimos entre eventos de destruição de árvores usados ​​para limitar explosões de folhagem. |
| `disableIllegalItemProtection` | bool | `false` | Desativa a proteção de item invalid/modded. |
| `disableButchering` | bool | `false` | Bloqueia o açougue de Pals. |
| `disableRenaming` | bool | `false` | Bloqueia a renomeação do jogador. |
| `disablePalRenaming` | bool | `false` | Bloqueia a renomeação de Pal. |
| `doActionUponIllegalPalStats` | bool | `true` | Aplica a ação de cheat configurada para estatísticas impossíveis de Pal. |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` | Bloqueia receitas não suportadas pelo ambiente de trabalho solicitado. |
| `preventDoctorSurgiExploit` | bool | `true` | Detects/blocks a exploração do Doutor Surgi. |
| `doActionUponDoctorSurgiExploit` | bool | `true` | Aplica a ação de trapaça configurada para esse exploit. |
| `palStatsMaxRank` | interno | `-1` | Classificação máxima de aprimoramento de Pal; `-1` usa limites de jogo automatic/current. |
| `bannedTechnologies` | array | Vazio | IDs de tecnologia bloqueados para aprendizagem e removidos quando detectados. |

## Opções de recursos anti-cheat

| Chave | Tipo | Padrão | Descrição |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` | Chave de compatibilidade para o recurso AntiDupe legado; inativo na versão atual. |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` | Intervalo mínimo legado entre builds; atualmente inativo. |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` | Intervalo mínimo legado entre desmontagens; atualmente inativo. |
| `antiDupeShowBlockMessage` | bool | `true` | Troca de mensagem de bloco herdada; atualmente inativo. |
| `antiDupeBuildMessage` | string | Texto gerado | Mensagem de bloco de construção herdada; atualmente inativo. |
| `antiDupeDismantleMessage` | string | Texto gerado | Mensagem herdada de bloqueio de desmontagem; atualmente inativo. |
| `antiVacuumEnabled` | bool | `true` | Ativa proteção de captação remota (vácuo). |
| `antiVacuumBlockAutoPickup` | bool | `true` | Aplica verificações anti-vácuo às coletas automáticas normais. |
| `antiVacuumBlockRelicObtain` | bool | `true` | Aplica verificações à coleção de relíquias. |
| `antiVacuumBlockNoteObtain` | bool | `true` | Aplica verificações à coleção de notas. |
| `antiVacuumBlockEggPickup` | bool | `true` | Aplica verificações à coleta de ovos. |
| `antiVacuumMaxPickupDistance` | float | `800.0` | Distância máxima de coleta permitida para solicitações protegidas. |
| `antiVacuumShowBlockMessage` | bool | `true` | Mostra uma mensagem voltada para o jogador quando uma coleta é bloqueada. |
| `antiVacuumBlockMessage` | string | Texto gerado | Mensagem mostrada para uma captura remota bloqueada. |
| `staminaCheatDetectionEnabled` | bool | `true` | Permite a detecção de ações de resistência suspeitas. |
| `baseCampDupeDetectionEnabled` | bool | `true` | Ativa a detecção de duplicação do acampamento base. |
| `damageCheatDetectionEnabled` | bool | `true` | Ativa a detecção de cheats de danos. |
| `damageCheatDetectionTolerancePercent` | float | `5.0` | Diferença percentual permitida entre o dano nativo relatado e o valor `BasePower × AttackWithBuff` reconstruído. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | float | `1.5` | Arma máxima permitida `BasePower` como um multiplicador da estática `AttackValue` da arma equipada. |
| `ammoCheatDetectionEnabled` | bool | `true` | Ativa a detecção de trapaças relacionadas à munição e ao estado da arma. |

As chaves `antiDupe...` ainda são geradas para compatibilidade de configuração, mas o recurso AntiDupe herdado está desabilitado na versão atual. Não confie nesses controles até que o recurso seja ativado novamente.

## Chaves de migração legadas

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS` e `PalImport_MaxIV` são somente leitura para migrar instalações mais antigas para [`Pals/ImportRules/Default.json`](./PalImportRules.md). Eles não são mais gravados nos arquivos `Config.json` atuais.

As antigas chaves `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd` e `blockTowerBossCapture` não fazem parte da configuração atual. Os registros de banimento pertencem a `Banlist.json`.
