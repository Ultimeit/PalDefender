### [<<<](README_ZH_CN.md) 命令

#### [English](./deletepals.md) / 简体中文

# /deletepals

| |权限|
|-|:---------:|
|仅管理员|X|
|聊天|X|
|RCON|X|

### 描述
根据过滤器从玩家的帕鲁队伍和帕鲁终端中删除多个帕鲁。过滤器可以通过命令参数配置。被删除的帕鲁将创建一个 .json 文件，以便在使用不当时恢复帕鲁。目前需要手动查找文件，未来版本计划提供一个恢复帕鲁的命令。

被删除的帕鲁可以在 `<palserver_root>/Pal/Binaries/Win64/PalDefender/pals/deleted/<SteamID>/` 中找到。

### 语法

```cmd
/deletepals <steamID> <PalFilter>
```

### PalFilter
该过滤器允许在一个命令行中使用多个关键字来删除符合条件的帕鲁。第一次使用时可能会比较复杂，所以请先在测试环境中尝试。

以下是过滤器关键字及其说明：
|关键字|值|符号|说明|
|-|:---------:|:---------:|-|
|ID|[PalID](../Data%20Lists/Pals.md) 或帕鲁列表|无|一个或多个 ID，使用 `,` 逗号分隔。不要用来忽略 ID 的过滤。|
|Nick|字符串|无|过滤帕鲁的名称。如果不需要，请不要使用。|
|Gender|`male` 或 `female`|无|按性别过滤。如果不需要过滤性别，请不要使用。|
|Level|数字|`<`, `>`, `<=`, `>=`, `=`, `!=`|按等级过滤。使用符号指定。例如，`Level>=35` 会包括等级为 35 及以上的帕鲁。|
|Rank|数字|`<`, `>`, `<=`, `>=`, `=`, `!=`|按排名过滤。使用符号指定。例如，`Rank>1` 会包括排名高于 1 的帕鲁。排名是根据相同帕鲁的综合排名。|
|Lucky|`true` 或 `false`|无|过滤是否为稀有（闪亮）伙伴。|
|Passives|[PassiveSkill](../Data%20Lists/PassiveSkills_ZH_CN.md) 或被动技能列表|无|一个或多个 ID，使用 `,` 逗号分隔。不要用来忽略技能的过滤。|
|Limit|数字|无|限制过滤结果的数量。例如，`Limit 5` 会使过滤器只找到 5 个帕鲁，即使可以找到更多。|

### 用法  
```cmd
/deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
```
这将删除最多 3 个等级高于 10 的帕鲁（因此等级为 10 或以下的帕鲁不会被删除），性别为男性，且帕鲁为滑水蛇或博爱蜥。
<br>
<br>
<br>

```cmd
/deletepals 76567890987654321 ID Anubis Rank >= 3
```
这将删除所有排名为 3 或以上的阿努比斯。
<br>
<br>
<br>

```cmd
/deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
```
这将删除拥有所有 4 个被动技能的帕鲁。

被动技能如下：
- CraftSpeed_up1 = Serious（认真）<br>
- CraftSpeed_up2 = Artisan（工匠精神）<br>
- Rare = Lucky（稀有）<br>
- PAL_CorporateSlave = Work Slave（社畜）<br>

因此，需要拥有这 4 个被动技能，如果只拥有 3 个，它将被忽略。