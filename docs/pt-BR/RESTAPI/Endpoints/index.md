# Pontos finais

> **Autenticação:** Token do portador (todos os endpoints abaixo)

> **Caminho base:** `/v1/pdapi`

> **Tipo de conteúdo:** `application/json` (para solicitações POST)

| Método | Ponto final | Descrição | Permissões | Detalhes                                             |
|--------------------------------------------------------|--------------------------------------------------|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| GET | `/v1/pdapi/players` | Liste todos os jogadores.             | `REST.Players.Read` | [GET /players](./players.md)                        |
| GET | `/v1/pdapi/player/<player_identifier>` | Mostre um jogador.              | `REST.Player.Read` | [GET /player](./player.md)                          |
| GET | `/v1/pdapi/pals/<player_identifier>` | Liste os Pals de um jogador.         | `REST.Pals.Read` | [GET /pals](./pals.md)                              |
| GET | `/v1/pdapi/items/<player_identifier>` | Liste os itens de um jogador.        | `REST.Items.Read` | [GET /items](./items.md)                            |
| GET | `/v1/pdapi/techs/<player_identifier>` | Liste as tecnologias de um jogador. | `REST.Techs.Read` | [GET /techs](./techs.md)                            |
| GET | `/v1/pdapi/progression/<player_identifier>` | Mostrar valores de progressão.      | `REST.Progression.Read` | [GET /progression](./progression.md)                |
| GET | `/v1/pdapi/guilds` | Listar guildas.                  | `REST.Guilds.Read` | [GET /guilds](./guilds.md)                          |
| GET | `/v1/pdapi/guild/<guild_id>` | Mostre uma guilda.               | `REST.Guild.Read` | [GET /guild](./guild.md)                            |
| GET | `/v1/pdapi/banlist` | Pesquisar registros de banimento.           | `REST.Banlist.Read` | [GET /banlist](./banlist.md)                        |
| GET | `/v1/pdapi/version` | Verifique API health/version. | `REST.Version.Read` | [GET /version](./version.md)                        |
| <span class='pd-badge pd-badge--deprecated'>Deprecated</span> POST | `/v1/pdapi/give` | Concessão de recompensa atômica legada. | Rota legada obsoleta. Use os pontos finais de recompensa dividida abaixo. | [POST /give deprecated](./give_deprecated.md) |
| POST | `/v1/pdapi/give/items/<player_identifier>` | Dê itens.                   | `REST.Items.Give` | [POST /give/items](./give-items.md)                 |
| POST | `/v1/pdapi/give/pals/<player_identifier>` | Dê Pals por ID.              | `REST.Pals.Give` | [POST /give/pals](./give-pals.md)                   |
| POST | `/v1/pdapi/give/paltemplate/<player_identifier>` | Dê modelos aos Pals.           | `REST.PalTemplates.Give` | [POST /give/paltemplate](./give-paltemplate.md)     |
| POST | `/v1/pdapi/give/paleggs/<player_identifier>` | Dê ovos ao Pal.                | `REST.PalEggs.Give` | [POST /give/paleggs](./give-paleggs.md)             |
| POST | `/v1/pdapi/give/progression/<player_identifier>` | Adicione EXP e pontos.           | `REST.Progression.Give` | [POST /give/progression](./give-progression.md)     |
| POST | `/v1/pdapi/summon/pal` | Gere um Pal nas coordenadas. | `REST.Summon.Pal` | [POST /summon/pal](./summon-pal.md) |
| POST | `/v1/pdapi/summon/npc` | Gere um NPC nas coordenadas. | `REST.Summon.NPC` | [POST /summon/npc](./summon-npc.md) |
| POST | `/v1/pdapi/learntech/<player_identifier>` | Aprenda tecnologias.           | `REST.Techs.Learn` | [POST /learntech](./learntech.md)                   |
| POST | `/v1/pdapi/forgettech/<player_identifier>` | Esqueça as tecnologias.          | `REST.Techs.Forget` | [POST /forgettech](./forgettech.md)                 |
| POST | `/v1/pdapi/deletebase/<base_camp_id>` | Delete a base/camp. | `REST.Base.Delete` | [POST /deletebase](./deletebase.md)                 |
| POST | `/v1/pdapi/ban/<player_identifier>` | Banir um usuário.                   | `REST.Punishments.Ban` | [POST /ban](./ban.md)                               |
| POST | `/v1/pdapi/unban/<user_id>` | Remova um banimento de usuário.            | `REST.Punishments.Unban` | [POST /unban](./unban.md)                           |
| POST | `/v1/pdapi/banip/<ip>` | Banir um IP.                    | `REST.Punishments.BanIP` | [POST /banip](./banip.md)                           |
| POST | `/v1/pdapi/unbanip/<ip>` | Remova uma proibição de IP.             | `REST.Punishments.UnbanIP` | [POST /unbanip](./unbanip.md)                       |
| POST | `/v1/pdapi/kick/<player_identifier>` | Chute um jogador.                | `REST.Punishments.Kick` | [POST /kick](./kick.md)                             |
| POST | `/v1/pdapi/SendPlayerMessage` | Envie mensagens aos jogadores.         | `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant` | [POST /SendPlayerMessage](./send-player-message.md) |
| POST | `/v1/pdapi/Broadcast` | Transmitir bate-papo.               | `REST.Messages.Broadcast` | [POST /Broadcast](./broadcast.md)                   |
| POST | `/v1/pdapi/Alert` | Envie um alerta.                | `REST.Messages.Alert` | [POST /Alert](./alert.md)                           |
| POST | `/v1/pdapi/ReloadConfig` | Recarregue a configuração.                | `REST.Reload.Config` | [POST /ReloadConfig](./reload-config.md)            |
