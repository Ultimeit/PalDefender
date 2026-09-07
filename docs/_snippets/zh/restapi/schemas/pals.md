### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Meta` | object | 目标玩家元数据及帕鲁数量。 |
| `Pals` | object | 目标玩家的队伍、帕鲁终端和基地帕鲁。 |

`Meta` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `PlayerUID` | string | Palworld 存档数据使用的玩家 UID。 |
| `Player` | string | 请求路径中提供的玩家标识符。 |
| `TeamCount` | integer | 玩家队伍中的帕鲁数量。 |
| `PalboxCount` | integer | 玩家帕鲁终端中的帕鲁数量。 |
| `BaseCampCount` | integer | 包含的基地数量。 |

`Pals` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `Team` | object | 以帕鲁实例 ID 为键的队伍帕鲁。 |
| `Palbox` | object | 以帕鲁实例 ID 为键的帕鲁终端帕鲁。 |
| `BaseCamps` | object[] | 公会基地及其分配的工作帕鲁。 |

帕鲁对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `PalID` | string | 帕鲁种类标识符。 |
| `UniqueNPCID` | string | 唯一 NPC ID（如果存在）。 |
| `Nickname` | string | 自定义帕鲁昵称；没有时为空字符串。 |
| `SkinId` | string | 皮肤 ID；没有时为空字符串。 |
| `Gender` | string | 帕鲁性别。 |
| `Level` | integer | 帕鲁等级。 |
| `Exp` | integer | 帕鲁经验值。 |
| `Shiny` | boolean | 是否为稀有帕鲁。 |
| `PartnerSkillLevel` | integer | 伙伴技能等级。 |
| `CondensedPals` | integer | 浓缩等级进度。 |
| `UnusedStatusPoints` | integer | 帕鲁未使用的属性点。 |
| `FriendshipPoints` | integer | 亲密度点数。 |
| `PhysicalHealth` | string | 身体健康状态。 |
| `WorkerSick` | string | 工作帕鲁的疾病状态。 |
| `ImportedCharacter` | boolean | 是否标记为已导入。 |
| `HP` | number | 当前生命值。 |
| `MP` | number | 当前魔力值（如果存在）。 |
| `SP` | number | 当前耐力值（如果存在）。 |
| `Shield` | number | 当前护盾值（如果存在）。 |
| `Hunger` | number | 当前饥饿值。 |
| `MaxHunger` | number | 最大饥饿值。 |
| `SAN` | number | 理智值。 |
| `Support` | integer | 支援值。 |
| `CraftSpeed` | integer | 制作速度值。 |
| `PalSouls` | object | 包含 `Health`、`Attack`、`Defense` 和 `CraftSpeed` 的帕鲁灵魂等级。 |
| `IVs` | object | 包含 `Health`、`AttackMelee`、`AttackShot` 和 `Defense` 的个体值。 |
| `ActiveSkills` | string[] | 已装备的主动技能。 |
| `LearntSkills` | string[] | 已学会的技能。 |
| `Passives` | string[] | 被动技能 ID。 |
| `ExtraWorkSuitabilities` | object | 以适应性 ID 为键的额外工作适应性等级。 |
| `DisableWorkPreferences` | string[] | 已禁用的工作偏好 ID。 |
| `team_slot_index` | integer | 队伍栏位索引，仅存在于 `Team` 帕鲁。 |
| `page` | integer | 帕鲁终端页面索引，仅存在于 `Palbox` 帕鲁。 |
| `slot` | integer | 帕鲁终端栏位索引，仅存在于 `Palbox` 帕鲁。 |
| `base_camp_slot_index` | integer | 基地工作帕鲁栏位索引，仅存在于基地帕鲁。 |

`BaseCamps[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `id` | string | 基地 GUID。 |
| `level` | integer | 基地等级。 |
| `world_pos` | object | 基地世界坐标。 |
| `map_pos` | object | 转换后的地图坐标。 |
| `state` | string | 当前基地状态。 |
| `pals` | object | 以帕鲁实例 ID 为键的基地工作帕鲁。 |

坐标对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `x` | number | X 坐标。 |
| `y` | number | Y 坐标。 |
| `z` | number | Z 坐标。 |
