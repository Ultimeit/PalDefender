# Points de terminaison

> **Auth :** Jeton du porteur (tous les points de terminaison ci-dessous)

> **Chemin de base :** `/v1/pdapi`

> **Type de contenu :** `application/json` (pour les requêtes POST)

| Méthode | Point de terminaison | Descriptif | Autorisations | Détails                                             |
|--------------------------------------------------------|--------------------------------------------------|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| GET | `/v1/pdapi/players` | Listez tous les joueurs.             | `REST.Players.Read` | [GET /players](./players.md)                        |
| GET | `/v1/pdapi/player/<player_identifier>` | Montrez un joueur.              | `REST.Player.Read` | [GET /player](./player.md)                          |
| GET | `/v1/pdapi/pals/<player_identifier>` | Répertoriez le Pals d'un joueur.         | `REST.Pals.Read` | [GET /pals](./pals.md)                              |
| GET | `/v1/pdapi/items/<player_identifier>` | Répertoriez les objets d'un joueur.        | `REST.Items.Read` | [GET /items](./items.md)                            |
| GET | `/v1/pdapi/techs/<player_identifier>` | Répertoriez les technologies d'un joueur. | `REST.Techs.Read` | [GET /techs](./techs.md)                            |
| GET | `/v1/pdapi/progression/<player_identifier>` | Afficher les valeurs de progression.      | `REST.Progression.Read` | [GET /progression](./progression.md)                |
| GET | `/v1/pdapi/guilds` | Liste des guildes.                  | `REST.Guilds.Read` | [GET /guilds](./guilds.md)                          |
| GET | `/v1/pdapi/guild/<guild_id>` | Montrez une guilde.               | `REST.Guild.Read` | [GET /guild](./guild.md)                            |
| GET | `/v1/pdapi/banlist` | Rechercher des enregistrements d'interdiction.           | `REST.Banlist.Read` | [GET /banlist](./banlist.md)                        |
| GET | `/v1/pdapi/version` | Cochez API health/version. | `REST.Version.Read` | [GET /version](./version.md)                        |
| <span class='pd-badge pd-badge--deprecated'>Deprecated</span> POST | `/v1/pdapi/give` | Subvention de récompense atomique héritée. | Itinéraire hérité obsolète. Utilisez les points de terminaison de récompense fractionnée ci-dessous. | [POST /give deprecated](./give_deprecated.md) |
| POST | `/v1/pdapi/give/items/<player_identifier>` | Donnez des objets.                   | `REST.Items.Give` | [POST /give/items](./give-items.md)                 |
| POST | `/v1/pdapi/give/pals/<player_identifier>` | Donnez Pals par pièce d'identité.              | `REST.Pals.Give` | [POST /give/pals](./give-pals.md)                   |
| POST | `/v1/pdapi/give/paltemplate/<player_identifier>` | Donnez le modèle Pals.           | `REST.PalTemplates.Give` | [POST /give/paltemplate](./give-paltemplate.md)     |
| POST | `/v1/pdapi/give/paleggs/<player_identifier>` | Donnez Pal œufs.                | `REST.PalEggs.Give` | [POST /give/paleggs](./give-paleggs.md)             |
| POST | `/v1/pdapi/give/progression/<player_identifier>` | Ajoutez de l'EXP et des points.           | `REST.Progression.Give` | [POST /give/progression](./give-progression.md)     |
| POST | `/v1/pdapi/summon/pal` | Générez un Pal aux coordonnées. | `REST.Summon.Pal` | [POST /summon/pal](./summon-pal.md) |
| POST | `/v1/pdapi/summon/npc` | Générez un NPC aux coordonnées. | `REST.Summon.NPC` | [POST /summon/npc](./summon-npc.md) |
| POST | `/v1/pdapi/learntech/<player_identifier>` | Apprenez les technologies.           | `REST.Techs.Learn` | [POST /learntech](./learntech.md)                   |
| POST | `/v1/pdapi/forgettech/<player_identifier>` | Oubliez les technologies.          | `REST.Techs.Forget` | [POST /forgettech](./forgettech.md)                 |
| POST | `/v1/pdapi/deletebase/<base_camp_id>` | Supprime une base ou un camp. | `REST.Base.Delete` | [POST /deletebase](./deletebase.md)                 |
| POST | `/v1/pdapi/ban/<player_identifier>` | Bannir un utilisateur.                   | `REST.Punishments.Ban` | [POST /ban](./ban.md)                               |
| POST | `/v1/pdapi/unban/<user_id>` | Supprimer une interdiction d'utilisateur.            | `REST.Punishments.Unban` | [POST /unban](./unban.md)                           |
| POST | `/v1/pdapi/banip/<ip>` | Interdire une IP.                    | `REST.Punishments.BanIP` | [POST /banip](./banip.md)                           |
| POST | `/v1/pdapi/unbanip/<ip>` | Supprimez une interdiction IP.             | `REST.Punishments.UnbanIP` | [POST /unbanip](./unbanip.md)                       |
| POST | `/v1/pdapi/kick/<player_identifier>` | Kick un joueur.                | `REST.Punishments.Kick` | [POST /kick](./kick.md)                             |
| POST | `/v1/pdapi/SendPlayerMessage` | Envoyez des messages aux joueurs.         | `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant` | [POST /SendPlayerMessage](./send-player-message.md) |
| POST | `/v1/pdapi/Broadcast` | Discussion diffusée.               | `REST.Messages.Broadcast` | [POST /Broadcast](./broadcast.md)                   |
| POST | `/v1/pdapi/Alert` | Envoyez une alerte.                | `REST.Messages.Alert` | [POST /Alert](./alert.md)                           |
| POST | `/v1/pdapi/ReloadConfig` | Recharger la configuration.                | `REST.Reload.Config` | [POST /ReloadConfig](./reload-config.md)            |
