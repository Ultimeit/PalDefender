# Permissions

> **Auth:** Bearer token required  
> **Base path:** `/v1/pdapi`  
> **Namespace:** `REST`

This table lists all REST API permissions and their associated functionality.

---

# 📋 Permissions Table

| Category        | Subcategory      | Action       | Permission ID |
|----------------|------------------|--------------|---------------|
| Players        | Players          | Read         | REST.Players.Read |
| Players        | Player           | Read         | REST.Player.Read |
| Pals           | Pals             | Read         | REST.Pals.Read |
| Pals           | Pals             | Give         | REST.Pals.Give |
| Items          | Items            | Read         | REST.Items.Read |
| Items          | Items            | Give         | REST.Items.Give |
| Progression    | Progression      | Read         | REST.Progression.Read |
| Progression    | Progression      | Give         | REST.Progression.Give |
| Techs          | Techs            | Read         | REST.Techs.Read |
| Techs          | Techs            | Learn        | REST.Techs.Learn |
| Techs          | Techs            | Forget       | REST.Techs.Forget |
| Guilds         | Guilds           | Read         | REST.Guilds.Read |
| Guilds         | Guild            | Read         | REST.Guild.Read |
| Banlist        | Banlist          | Read         | REST.Banlist.Read |
| Punishments    | Punishments      | Ban          | REST.Punishments.Ban |
| Punishments    | Punishments      | Unban        | REST.Punishments.Unban |
| Punishments    | Punishments      | Ban IP       | REST.Punishments.BanIP |
| Punishments    | Punishments      | Unban IP     | REST.Punishments.UnbanIP |
| Punishments    | Punishments      | Kick         | REST.Punishments.Kick |
| Base           | Base             | Delete       | REST.Base.Delete |
| Pal            | Templates        | Give         | REST.PalTemplates.Give |
| Pal            | Eggs             | Give         | REST.PalEggs.Give |
| Messages       | Send             | Player Chat  | REST.Messages.Send.PlayerChat |
| Messages       | Send             | Global Chat  | REST.Messages.Send.GlobalChat |
| Messages       | Send             | Guild Chat   | REST.Messages.Send.GuildChat |
| Messages       | Send             | Log Normal   | REST.Messages.Send.Log.Normal |
| Messages       | Send             | Log Important| REST.Messages.Send.Log.Important |
| Messages       | Send             | Log Very Important | REST.Messages.Send.Log.VeryImportant |
| Messages       | Messages         | Broadcast    | REST.Messages.Broadcast |
| Messages       | Messages         | Alert        | REST.Messages.Alert |
| System         | Version          | Read         | REST.Version.Read |
| System         | Reload           | Config       | REST.Reload.Config |

---

## 📌 Notes

- Each permission controls access to a specific REST endpoint action
- Missing permissions will result in HTTP 403 Forbidden
- Some endpoints require multiple permissions (e.g. messaging logs)