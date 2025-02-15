### [<<<](README.md) File Types

#### English / [简体中文](./PalJSON_ZH_CN.md)

# PalJSON

### Contents
- [Description](PalJSON.md#description)
- [Attributes](PalJSON.md#attributes)
- [Template](PalJSON.md#template)
- [Presets](PalJSON.md#presets)

## Description
PalJSON is a JSON file that defines the attributes for the Pal being created. **It must include a `CharacterID`, otherwise, the creation process will fail.**

Check this out for default values: [GitHub/iiLarsH/Chillet/csv's/PalData.csv](https://github.com/iiLarsH/Chillet/blob/698b5ea1190177533dc7924f9af9e40ff8ee4776/csv's/PalData.csv)

## Attributes

|Key|Value Type|Value(s)|Description|
|---|----------|--------|-----------|
|`CharacterID`|String containing [PalID](https://pwmodding.wiki/docs/game-data/monster-table)|"..."|Determines which Pal it is.|
|`NickName`|String|"..."|Display Name of the Pal.|
|`UniqueNPCID`|String|"..."||
|`Gender`|Integer|1 = Male<br>2 = Female||
|`Level`|Integer|0 - 255|The level of the Pal.|
|`Exp`|Integer|0 to 2^63|The amount of exp the Pal has.|
|`IsRarePal`|Boolean|true or false|Shiny flag.
|`MaxHP`|Integer|0 to 2^63|The max HP of the Pal.|
|`Hp`|Integer|0 to 2^63|The current HP of the Pal.|
|`MaxMP`|Integer|0 to 2^63|The max MP of the Pal.|
|`MP`|Integer|0 to 2^63|The current MP of the Pal.|
|`MaxSP`|Integer|0 to 2^63|The max SP of the Pal.|
|`ShieldMaxHP`|Integer|0 to 2^63|The max Shield HP of the Pal.|
|`ShieldHP`|Integer|0 to 2^63|The current Shield HP of the Pal.|
|`FullStomach`|Float|0.0 to ??|The Pal's current stomach fullness.|
|`MaxFullStomach`|Float|0.0 to ??|The Pal's max stomach . Heighest default Value I found on a Pal was `600.0`.|
|`Support`|Integer|0 to 2^31||
|`CraftSpeed`|Integer|0 to 2^31|The Pal's base crafting speed. Default is `100`.|
|`SanityValue`|Float|0.0 to ??|The current Pal's SAN.|
|`UnusedStatusPoint`|Integer|0 to 2^16||
|`Rank`|Integer|0 - 255|
|`RankUpExp`|Integer|0 - 255|
|`Rank_HP`|Integer|0 - 255|
|`Rank_Attack`|Integer|0 - 255|
|`Rank_Defence`|Integer|0 - 255|
|`Rank_CraftSpeed`|Integer|0 - 255|
|`Talent_HP`|Integer|0 - 255|
|`Talent_Melee`|Integer|0 - 255|
|`Talent_Shot`|Integer|0 - 255|
|`Talent_Defense`|Integer|0 - 255|
|`EquipWaza`|String Array of [EPalWazaIDs](../Data%20Lists/EPalWazaIDs.md)|["", "", ""]|The active/equipped Skills of the Pal.|
|`MasteredWaza`|String Array of [EPalWazaIDs](../Data%20Lists/EPalWazaIDs.md)|["", "", "", ""]|The learned Skills of the Pal.|
|`PassiveSkillList`|String Array of [PassiveSkills](../Data%20Lists/PassiveSkills.md)|["", "", "", ""]|All passive Skills the Pal has.|


## Template
The files have to be placed in [`Pal/Binaries/Win64/PalDefender/pals/`](../../README.md#windows)
```json
{
    "NickName": "",
    "CharacterID": "",
    "UniqueNPCID": "",
    "Gender": 1,
    "Level": 1,
    "Exp": 0,
    "IsRarePal": false,
    "MaxHP": 100,
    "Hp": 100,
    "MaxMP": 100,
    "MP": 100,
    "MaxSP": 100,
    "ShieldMaxHP": 0,
    "ShieldHP": 0,
    "FullStomach": 600.0,
    "MaxFullStomach": 600.0,
    "Support": 100,
    "CraftSpeed": 100,
    "SanityValue": 100.0,
    "UnusedStatusPoint": 0,
    "Rank": 0,
    "RankUpExp": 0,
    "Rank_HP": 0,
    "Rank_Attack": 0,
    "Rank_Defence": 0,
    "Rank_CraftSpeed": 0,
    "Talent_HP": 0,
    "Talent_Melee": 0,
    "Talent_Shot": 0,
    "Talent_Defense": 0,
    "EquipWaza": [],
    "MasteredWaza": [],
    "PassiveSkillList": []
}
```

## Presets
* [OPnubis](PalJSON%20Presets/OPnubis.json) - Anubis with absolute maxed out attributes.
