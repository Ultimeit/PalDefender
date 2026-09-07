### 200 响应架构

| 字段 | 类型 | 描述 |
|---|---|---|
| `Guild` | object | 公会详情。 |

`Guild` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `name` | string | 公会名称。 |
| `Level` | integer | 公会基地等级。 |
| `admin` | object | 公会管理员详情。 |
| `member_count` | integer | 公会成员数量。 |
| `members` | object[] | 详细的公会成员记录。 |
| `camp_count` | integer | 公会中的基地数量。 |
| `camps` | object[] | 详细的基地记录。 |
| `items` | object | 公会物品储存数据。 |
| `expeditions` | object | 公会远征数据。 |
| `laboratory` | object | 公会实验室研究数据。 |

`admin` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `id` | string | 管理员 PlayerUID。 |
| `name` | string | 管理员玩家名称。 |

`members[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `player_uid` | string | 成员 PlayerUID。 |
| `player_name` | string | 成员玩家名称。 |
| `status` | string | 成员状态。 |

`camps[]` 条目架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `id` | string | 基地 GUID。 |
| `level` | integer | 基地等级。 |
| `world_pos` | object | 基地世界坐标。 |
| `map_pos` | object | 转换后的地图坐标。 |
| `state` | string | 当前基地状态。 |
| `pals` | object | 以帕鲁实例 ID 为键的基地工作帕鲁。 |
| `buildings` | string | 当前建筑载荷占位符。 |

坐标对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `x` | number | X 坐标。 |
| `y` | number | Y 坐标。 |
| `z` | number | Z 坐标。 |

基地帕鲁对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `nickname` | string | 帕鲁昵称。 |
| `pal_id` | string | 帕鲁种类标识符。 |
| `npc_id` | string | 唯一 NPC ID。 |
| `skin_id` | string | 皮肤 ID。 |
| `gender` | string | 帕鲁性别。 |
| `level` | integer | 帕鲁等级。 |
| `shiny` | boolean | 是否为稀有帕鲁。 |
| `phisical_health` | string | 当前 API 返回的身体健康状态。 |
| `worker_sick` | string | 工作帕鲁的疾病状态。 |
| `san` | number | 理智值。 |
| `imported` | boolean | 是否标记为已导入。 |
| `friendship` | integer | 亲密度点数。 |
| `active_skills` | string[] | 已装备的主动技能。 |
| `learnt_skills` | string[] | 已学会的技能。 |
| `passives` | string[] | 被动技能 ID。 |

`items` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `container_id` | string | 公会物品容器 ID（如果可用）。 |
| `current` | integer | 已占用栏位数。 |
| `max` | integer | 栏位总数。 |
| `<slot_index>` | object | 以数字栏位索引为键的栏位物品对象。 |

公会物品栏位对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `item_id` | string | 栏位中的物品 ID。 |
| `count` | integer | 栏位中的堆叠数量。 |

`expeditions` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `finished` | integer | 已完成的远征数量。 |
| `missions` | object | 以任务 ID 为键的已解锁任务标记。 |

`laboratory` 对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `current_research` | string | 当前研究 ID。 |
| `researches` | object | 以研究 ID 为键的进行中研究进度。 |

研究进度对象架构：

| 字段 | 类型 | 描述 |
|---|---|---|
| `work_amount` | number | 当前工作量。 |
| `required_work_amount` | number | 所需工作量。 |
| `percentage` | number | 当前工作量除以所需工作量。 |
