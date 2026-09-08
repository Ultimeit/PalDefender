# エンドポイント

> **認証:** ベアラー トークン (以下のすべてのエンドポイント)

> **ベースパス:** `/v1/pdapi`

> **コンテンツ タイプ:** `application/json` (POST リクエストの場合)

|方法 |エンドポイント |説明 |権限 |詳細 |
|--------------------------------------------------------|--------------------------------------------------|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------|
| GET | `/v1/pdapi/players` |すべてのプレイヤーをリストします。             | `REST.Players.Read` | [GET /players](./players.md) |
| GET | `/v1/pdapi/player/<player_identifier>` |プレイヤーを 1 人表示します。              | `REST.Player.Read` | [GET /player](./player.md) |
| GET | `/v1/pdapi/pals/<player_identifier>` |プレーヤーの Pals をリストします。         | `REST.Pals.Read` | [GET /pals](./pals.md) |
| GET | `/v1/pdapi/items/<player_identifier>` |プレイヤーのアイテムをリストします。        | `REST.Items.Read` | [GET /items](./items.md) |
| GET | `/v1/pdapi/techs/<player_identifier>` |プレイヤーのテクノロジーを列挙します。 | `REST.Techs.Read` | [GET /techs](./techs.md) |
| GET | `/v1/pdapi/progression/<player_identifier>` |進行値を表示します。      | `REST.Progression.Read` | [GET /progression](./progression.md) |
| GET | `/v1/pdapi/guilds` |ギルドをリストします。                  | `REST.Guilds.Read` | [GET /guilds](./guilds.md) |
| GET | `/v1/pdapi/guild/<guild_id>` |ギルドを 1 つ表示します。               | `REST.Guild.Read` | [GET /guild](./guild.md) |
| GET | `/v1/pdapi/banlist` |禁止記録を検索します。           | `REST.Banlist.Read` | [GET /banlist](./banlist.md) |
| GET | `/v1/pdapi/version` | API の健全性/バージョンを確認します。     | `REST.Version.Read` | [GET /version](./version.md) |
| <span class='pd-badge pd-badge--deprecated'>非推奨</span> POST | `/v1/pdapi/give` |レガシーのアトミック報酬付与。 |廃止されたレガシー ルート。以下の分割報酬エンドポイントを使用します。 | [POST /give は非推奨になりました](./give_deprecated.md) |
| POST | `/v1/pdapi/give/items/<player_identifier>` |アイテムを付与します。                   | `REST.Items.Give` | [POST /give/items](./give-items.md) |
| POST | `/v1/pdapi/give/pals/<player_identifier>` | ID を指定して Pal を付与します。              | `REST.Pals.Give` | [POST /give/pals](./give-pals.md) |
| POST | `/v1/pdapi/give/paltemplate/<player_identifier>` |テンプレートから Pal を付与します。           | `REST.PalTemplates.Give` | [POST /give/paltemplate](./give-paltemplate.md) |
| POST | `/v1/pdapi/give/paleggs/<player_identifier>` | Pal の卵を付与します。                | `REST.PalEggs.Give` | [POST /give/paleggs](./give-paleggs.md) |
| POST | `/v1/pdapi/give/progression/<player_identifier>` | EXP とポイントを追加します。           | `REST.Progression.Give` | [POST /give/progression](./give-progression.md) |
| POST | `/v1/pdapi/summon/pal` |座標で Pal を生成します。 | `REST.Summon.Pal` | [POST /summon/pal](./summon-pal.md) |
| POST | `/v1/pdapi/summon/npc` |座標で NPC を生成します。 | `REST.Summon.NPC` | [POST /summon/npc](./summon-npc.md) |
| POST | `/v1/pdapi/learntech/<player_identifier>` |テクノロジーを習得させます。           | `REST.Techs.Learn` | [POST /learntech](./learntech.md) |
| POST | `/v1/pdapi/forgettech/<player_identifier>` |テクノロジーを未習得に戻します。          | `REST.Techs.Forget` | [POST /forgettech](./forgettech.md) |
| POST | `/v1/pdapi/deletebase/<base_camp_id>` |基地/キャンプを削除します。           | `REST.Base.Delete` | [POST /deletebase](./deletebase.md) |
| POST | `/v1/pdapi/ban/<player_identifier>` |ユーザーを禁止します。                   | `REST.Punishments.Ban` | [POST /ban](./ban.md) |
| POST | `/v1/pdapi/unban/<user_id>` |ユーザーの禁止を解除します。            | `REST.Punishments.Unban` | [POST /unban](./unban.md) |
| POST | `/v1/pdapi/banip/<ip>` | IP を禁止します。                    | `REST.Punishments.BanIP` | [POST /banip](./banip.md) |
| POST | `/v1/pdapi/unbanip/<ip>` | IP 禁止を解除します。             | `REST.Punishments.UnbanIP` | [POST /unbanip](./unbanip.md) |
| POST | `/v1/pdapi/kick/<player_identifier>` |プレイヤーをキックします。                | `REST.Punishments.Kick` | [POST /kick](./kick.md) |
| POST | `/v1/pdapi/SendPlayerMessage` |プレイヤーにメッセージを送信します。         | `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant` | [POST /SendPlayerMessage](./send-player-message.md) |
| POST | `/v1/pdapi/Broadcast` |ブロードキャストチャット。               | `REST.Messages.Broadcast` | [POST /Broadcast](./broadcast.md) |
| POST | `/v1/pdapi/Alert` |アラートを送信します。                | `REST.Messages.Alert` | [POST /Alert](./alert.md) |
| POST | `/v1/pdapi/ReloadConfig` |設定をリロードします。                | `REST.Reload.Config` | [POST /ReloadConfig](./reload-config.md) |
