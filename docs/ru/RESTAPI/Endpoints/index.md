# Конечные точки

> **Аутентификация:** Токен носителя (все конечные точки ниже)

> **Базовый путь:** `/v1/pdapi`

> **Тип контента:** `application/json` (для запросов POST)

| Метод | Конечная точка | Описание | Разрешения | Подробности                                             |
|--------------------------------------------------------|--------------------------------------------------|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| GET | `/v1/pdapi/players` | Перечислите всех игроков.             | `REST.Players.Read` | [GET /players](./players.md)                        |
| GET | `/v1/pdapi/player/<player_identifier>` | Покажите одного игрока.              | `REST.Player.Read` | [GET /player](./player.md)                          |
| GET | `/v1/pdapi/pals/<player_identifier>` | Перечислите Pals игрока.         | `REST.Pals.Read` | [GET /pals](./pals.md)                              |
| GET | `/v1/pdapi/items/<player_identifier>` | Перечислите предметы игрока.        | `REST.Items.Read` | [GET /items](./items.md)                            |
| GET | `/v1/pdapi/techs/<player_identifier>` | Перечислите технологии игрока. | `REST.Techs.Read` | [GET /techs](./techs.md)                            |
| GET | `/v1/pdapi/progression/<player_identifier>` | Показать значения прогрессии.      | `REST.Progression.Read` | [GET /progression](./progression.md)                |
| GET | `/v1/pdapi/guilds` | Список гильдий.                  | `REST.Guilds.Read` | [GET /guilds](./guilds.md)                          |
| GET | `/v1/pdapi/guild/<guild_id>` | Покажите одну гильдию.               | `REST.Guild.Read` | [GET /guild](./guild.md)                            |
| GET | `/v1/pdapi/banlist` | Поиск записей о запрете.           | `REST.Banlist.Read` | [GET /banlist](./banlist.md)                        |
| GET | `/v1/pdapi/version` | Проверьте API health/version. | `REST.Version.Read` | [GET /version](./version.md)                        |
| <span class='pd-badge pd-badge--deprecated'>Deprecated</span> POST | `/v1/pdapi/give` | Наследие атомной награды. | Устаревший устаревший маршрут. Используйте конечные точки разделения вознаграждения ниже. | [POST /give deprecated](./give_deprecated.md) |
| POST | `/v1/pdapi/give/items/<player_identifier>` | Дайте предметы.                   | `REST.Items.Give` | [POST /give/items](./give-items.md)                 |
| POST | `/v1/pdapi/give/pals/<player_identifier>` | Дайте Pals по идентификатору.              | `REST.Pals.Give` | [POST /give/pals](./give-pals.md)                   |
| POST | `/v1/pdapi/give/paltemplate/<player_identifier>` | Дайте шаблон Pals.           | `REST.PalTemplates.Give` | [POST /give/paltemplate](./give-paltemplate.md)     |
| POST | `/v1/pdapi/give/paleggs/<player_identifier>` | Дайте Pal яиц.                | `REST.PalEggs.Give` | [POST /give/paleggs](./give-paleggs.md)             |
| POST | `/v1/pdapi/give/progression/<player_identifier>` | Добавьте EXP и очки.           | `REST.Progression.Give` | [POST /give/progression](./give-progression.md)     |
| POST | `/v1/pdapi/summon/pal` | Создайте Pal по координатам. | `REST.Summon.Pal` | [POST /summon/pal](./summon-pal.md) |
| POST | `/v1/pdapi/summon/npc` | Создайте NPC по координатам. | `REST.Summon.NPC` | [POST /summon/npc](./summon-npc.md) |
| POST | `/v1/pdapi/learntech/<player_identifier>` | Изучайте технологии.           | `REST.Techs.Learn` | [POST /learntech](./learntech.md)                   |
| POST | `/v1/pdapi/forgettech/<player_identifier>` | Забудьте о технологиях.          | `REST.Techs.Forget` | [POST /forgettech](./forgettech.md)                 |
| POST | `/v1/pdapi/deletebase/<base_camp_id>` | Delete и base/camp. | `REST.Base.Delete` | [POST /deletebase](./deletebase.md)                 |
| POST | `/v1/pdapi/ban/<player_identifier>` | Заблокировать пользователя.                   | `REST.Punishments.Ban` | [POST /ban](./ban.md)                               |
| POST | `/v1/pdapi/unban/<user_id>` | Снять бан пользователя.            | `REST.Punishments.Unban` | [POST /unban](./unban.md)                           |
| POST | `/v1/pdapi/banip/<ip>` | Запретить IP.                    | `REST.Punishments.BanIP` | [POST /banip](./banip.md)                           |
| POST | `/v1/pdapi/unbanip/<ip>` | Снять бан по IP.             | `REST.Punishments.UnbanIP` | [POST /unbanip](./unbanip.md)                       |
| POST | `/v1/pdapi/kick/<player_identifier>` | Ударить игрока.                | `REST.Punishments.Kick` | [POST /kick](./kick.md)                             |
| POST | `/v1/pdapi/SendPlayerMessage` | Отправляйте сообщения игрокам.         | `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant` | [POST /SendPlayerMessage](./send-player-message.md) |
| POST | `/v1/pdapi/Broadcast` | Трансляция чата.               | `REST.Messages.Broadcast` | [POST /Broadcast](./broadcast.md)                   |
| POST | `/v1/pdapi/Alert` | Отправьте оповещение.                | `REST.Messages.Alert` | [POST /Alert](./alert.md)                           |
| POST | `/v1/pdapi/ReloadConfig` | Перезагрузить конфигурацию.                | `REST.Reload.Config` | [POST /ReloadConfig](./reload-config.md)            |
