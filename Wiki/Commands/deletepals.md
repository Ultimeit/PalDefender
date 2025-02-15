### [<<<](README.md) Commands

#### English / [简体中文](./deletepals_ZH_CN.md)

# /deletepals

| |Permissions|
|-|:---------:|
|Admin Only|X|
|Chat|X|
|RCON|X|

### Description
Deletes multiple pals from a player's palteam and palbox based on a filter, which can be configured through command arguments. Deleted pals will create a .json file so you can restore pals upon invalid usage. This requires manual file lookup for now. A counter command to restore pals is planned in a future release.

The delete pals can be found in `<palserver_root>/Pal/Binaries/Win64/PalDefender/pals/deleted/<SteamID>/`.

### Syntax

```cmd
/deletepals <steamID> <PalFilter>
```

### PalFilter
The filter allows multiple keywords in one commandline to delete pals by the filter. It is very complex to understand on first try, so please try it in a test environment first.

Following filter keywords exist:
|Keyword|Values|Symbols|Explanation|
|-|:---------:|:---------:|-|
|ID|[PalID](../Data%20Lists/Pals.md) or list of [PalID](../Data%20Lists/Pals.md)s|None|One or more IDs separated by a `,` comma. Dont use to ignore ID in the filter.|
|Nick|String|None|the name of the pals to filter. dont use if not needed.|
|Gender|`male` or `female`|None|adds a filter by male or female. dont use if you want both.|
|Level|Number|`<`, `>`, `<=`, `>=`, `=`, `!=`|Filter by level. Use a symbol to specify. `Level>=35` will include pals at lvl 35 and higher.|
|Rank|Number|`<`, `>`, `<=`, `>=`, `=`, `!=`|Filter by rank. Use a symbol to specify. `Rank>1` will include pals which rank is above 1. Rank means the rank by combining the same pal.|
|Lucky|`true` or `false`|None|Filter if the pal should have or not have the lucky flag. Also known as "shiny".|
|Passives|[PassiveSkill](../Data%20Lists/PassiveSkills.md) or list of [PassiveSkill](../Data%20Lists/PassiveSkills.md)s|None|One or more IDs separated by a `,` comma. Dont use to ignore ID in the filter.|
|Limit|Number|None|A max limit of how many pals to filter. `Limit 5` would only allow the filter to find 5 pals even tho it could grab way more.|

### Usage
```cmd
/deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
```
This will delete max 3 pals which level is higher than 10 (so lvl 10 and below wont be deleted), gender is male and the pal ID is Serpent or PinkLizard.
<br>
<br>
<br>

```cmd
/deletepals 76567890987654321 ID Anubis Rank >= 3
```
This will delete every Anubis which Rank is 3 or above 3.
<br>
<br>
<br>

```cmd
/deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
```
This deletes every pal that has all 4 passives.

Passives are:
- CraftSpeed_up1 = Serious<br>
- CraftSpeed_up2 = Artisan<br>
- Rare = Lucky<br>
- PAL_CorporateSlave = Work Slave<br>

so it needs all 4 passives, if it has only 3 it will be ignored.