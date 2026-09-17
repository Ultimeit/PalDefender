# 📄 `PalSummon.json`

PalSummon 파일은 `/summon <filename>`으로 시작하는 고정 위치 전투 이벤트를 정의합니다. 파일은 `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/`에, 참조하는 PalTemplate은 `Pals/Templates/`에 저장하세요.

!!! tip "ID 조회"
    참조하는 템플릿의 `PalID`는 [paldeck.cc/pals](https://paldeck.cc/pals), 패시브는 [paldeck.cc/passives](https://paldeck.cc/passives), 기술 ID는 [paldeck.cc/skills](https://paldeck.cc/skills)에서 확인하세요.

## 전투 이벤트 설정 키

| 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `PalTemplate` | 문자열 | 필수 | `Pals/Templates/`에 있는 템플릿 파일 이름입니다. `.json`은 생략할 수 있습니다. |
| `BossBattleName` | 문자열 | 팰 ID | 공지, 로그, 웹훅, 피해량 결과에 표시할 이름입니다. |
| `Uncapturable` | 불리언 | `false` | 소환된 팰을 어떤 경우에도 포획할 수 없게 합니다. |
| `CapturableAtHealthPercent` | 숫자 | `15` | 포획 가능한 팰은 체력 비율이 이 값 이하일 때만 포획할 수 있습니다(`0`–`100`). `Uncapturable`이 `true`이면 무시됩니다. |
| `DisableAI` | 불리언 | `false` | 일반 AI를 끕니다. 회피 등의 일부 반응 행동은 여전히 발생할 수 있습니다. |
| `DisableDamageMeter` | 불리언 | `false` | 피해량 집계, 결과 창, 순위 보상을 끕니다. 대신 모든 접속 중인 플레이어에게 `Default` 보상을 지급합니다. |
| `SpawnScale` | 숫자 | `1.0` | 외형 및 물리적 크기 배율입니다. 0 이하이면 `1.0`을 사용합니다. |
| `DamageTakenMultiplier` | 숫자 | `1.0` | 받는 피해량 배율입니다. 음수이면 `1.0`을 사용합니다. |
| `DamageDealtMultiplier` | 숫자 | `1.0` | 주는 피해량 배율입니다. 음수이면 `1.0`을 사용합니다. |
| `X`, `Y`, `Z` | 숫자 | 필수 | 맵 좌표입니다. `/getpos`로 확인하세요. |
| `DisableStatuses` | 배열 | 비어 있음 | 적용을 막을 상태 이름입니다. 잘못된 이름은 건너뜁니다. |
| `Rewards` | 객체 또는 배열 | 비어 있음 | 선택적으로 설정하는 순위별 및 기본 [보상 정의](#damage-meter-and-rewards)입니다. 객체 형식을 권장합니다. |

호환성을 위해 `CapturableAt`, `CapturableAtPercent`, `capturable_at`도 별칭으로 허용합니다. `AdditionalEnemyReceiveDamageRate`와 `AdditionalEnemyInflictDamageRate`도 사용할 수 있지만, 표에 있는 이름을 권장합니다.

!!! warning "최대 체력 설정 변경"
    소환된 팰의 최대 체력은 이제 참조하는 PalTemplate의 `HP`에서 가져옵니다. `HealthMultiplier`, `HPMultiplier`, `AdditionalEnemyMaxHPRate`는 더 이상 지원하지 않으므로 기존 PalSummon 파일에서 제거하세요.

## 피해량 집계 및 보상 { #damage-meter-and-rewards }

소환된 팰이 죽거나 포획되면 보상을 결정합니다. 피해량 순위는 높은 순서로 정렬됩니다. 결과 창에는 상위 5명을 표시하고 상위 3명을 강조하며, 결과를 받는 플레이어가 5위 밖이면 자신의 순위도 표시합니다.

피해량 집계를 켜면 각 참가자의 보상을 다음과 같이 처리합니다.

1. `Rewards`에서 플레이어의 최종 순위에 해당하는 숫자 키를 찾습니다.
2. 해당 순위 키가 없으면 `Rewards.Default`를 사용합니다.
3. 둘 다 없으면 해당 플레이어는 보상을 받지 않습니다.
4. 선택한 보상은 플레이어별로 따로 추첨합니다. 같은 `Default` 정의를 사용하더라도 두 플레이어가 서로 다른 무작위 결과를 받을 수 있습니다.

이벤트가 끝날 때 여전히 접속 중이고 사용 가능한 플레이어 컨트롤러가 있는 참가자만 순위 보상을 받을 수 있습니다. 숫자 키의 보상은 `Default` 보상에 추가되는 것이 아니라 해당 순위의 기본 보상을 대체합니다.

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

이 예제에서 1위는 확정 보상 두 개를 모두 받고, 2위는 무작위 양의 경험치를 받습니다. 나머지 순위 참가자는 각각 독립적으로 75% 확률로 `Money` 1,000개를 받습니다.

순위 키는 `"1"`, `"2"`, `"10"`처럼 JSON 객체 키로 작성한 양의 정수여야 합니다. `"0"`, 음수 순위, 임의의 이름은 사용할 수 없습니다. `Default`는 대소문자를 구분하지 않습니다.

??? note "배열 형식"
    `Rewards`는 배열로도 작성할 수 있습니다. 인덱스 0은 1위, 인덱스 1은 2위에 해당합니다. 배열 형식에서는 `Default`를 정의할 수 없으므로 더 명확한 객체 형식을 권장합니다.

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### 보상 정의 구조

각 순위와 `Default`에는 하나의 보상 정의가 들어갑니다. 다음 두 항목을 함께 포함할 수 있습니다.

- `Drops`: 각 항목을 직접, 독립적으로 판정합니다.
- `Pools`: 항목을 선택하는 방식을 제어하는 보상 그룹입니다.

성장 보상의 단축 필드인 `EXP`, `TechnologyPoints`, `AncientTechnologyPoints`도 포함할 수 있습니다. 단축 필드는 확정 지급되며 별도의 `Chance`, `Weight`, `Unique` 설정이 필요 없을 때 유용합니다.

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### 보상 항목 유형

각 항목에는 보상 유형을 정확히 하나만 지정해야 합니다. 같은 항목에 아이템, 알, 성장 보상 필드를 함께 넣지 마세요.

| 보상 | 필수 필드 | 선택 필드 | 참고 |
| --- | --- | --- | --- |
| 아이템 | `ItemID` | `Count`, `Chance`, `Weight`, `Unique` | `Count`의 기본값은 `1`입니다. |
| 팰 알 | `EggID`, `PalTemplate` | `Count`, `Level`, `Chance`, `Weight`, `Unique` | `Count`의 기본값은 `1`이며, `Level: 0`은 템플릿의 레벨을 사용합니다. |
| 경험치 | `EXP` | `Chance`, `Weight`, `Unique` | `EXP` 값에 지급량 또는 범위를 지정합니다. |
| 기술 포인트 | `TechnologyPoints` | `Chance`, `Weight`, `Unique` | 필드 값에 지급량 또는 범위를 지정합니다. |
| 고대 기술 포인트 | `AncientTechnologyPoints` | `Chance`, `Weight`, `Unique` | 필드 값에 지급량 또는 범위를 지정합니다. |

`Chance`, `Weight`, `Unique`는 아래에서 설명하는 조건에서만 적용됩니다. 파서가 필드를 허용하더라도 모든 지급 모드에서 효과가 있는 것은 아닙니다.

위의 정식 필드 이름을 권장합니다. 다음 별칭도 허용됩니다.

| 정식 필드 | 허용되는 별칭 |
| --- | --- |
| `ItemID` | `ItemId`, `ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`, `Num` |
| `EXP` | `Exp`, `Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### 고정값, 범위 및 확률

지급량은 고정 정수 또는 양 끝값을 포함하는 범위로 지정할 수 있습니다.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- `Count`, 경험치, 기술 포인트 지급량은 `1` 이상의 정수여야 합니다.
- 범위에는 `Min`과 `Max`가 모두 필요하며, `Max`는 `Min`보다 작을 수 없습니다.
- `"1-3"` 같은 문자열 범위는 사용할 수 없습니다. `{ "Min": 1, "Max": 3 }`을 사용하세요.
- 알의 `Level`을 `0`으로 지정하면 참조하는 PalTemplate의 레벨을 유지합니다. 양수이면 템플릿 레벨을 대체하며, 지급 시 최대 255로 제한됩니다.
- `Chance`에는 숫자 또는 숫자 문자열을 사용할 수 있으며, 문자열에는 `%`를 붙일 수 있습니다. 예: `30`, `30.5`, `"30%"`.
- `Chance: 0`은 항상 실패하고 `Chance: 100`은 항상 성공합니다. 값은 `0`에서 `100` 사이여야 합니다.
- 확률이 0 초과 100 미만이면 추첨값이 설정값보다 작아야 성공합니다. 따라서 추첨값이 정확히 `30.0`이면 `Chance: 30`에서는 실패합니다.

### 직접 지급 보상

`Drops`의 각 항목은 독립적으로 판정합니다. 인접한 항목 중 하나만 선택하는 방식이 아닙니다. `Chance`를 생략하면 `100`을 사용합니다.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

`Money`는 확정 지급됩니다. 탄약, 경험치, 기술 포인트는 각각 따로 추첨하므로 선택 보상 세 개 중 아무것도 받지 않거나, 하나·둘·셋 모두 받을 수 있습니다.

직접 지급하는 `Drops`에서는 `Weight`와 `Unique`가 적용되지 않으며 경고가 발생합니다. 확률형 직접 보상에는 `Chance`를 사용하세요.

## 보상 풀

보상 풀은 먼저 자체 `Chance`를 판정합니다. 실패하면 풀 안의 항목은 판정하지 않습니다. 성공하면 `Mode`에 따라 항목을 처리합니다.

| 풀 설정 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `Name` | 문자열 | 비어 있음 | 문제 확인용 이름입니다. 선택 사항이며 추첨에는 영향을 주지 않습니다. |
| `Mode` | 문자열 | `OneOf` | `OneOf`, `Pick`, `All`, `Independent` 중 하나입니다. 대소문자를 구분하지 않습니다. |
| `Chance` | 숫자 또는 백분율 문자열 | `100` | 보상 풀 전체가 활성화될 확률입니다. |
| `Rolls` | 정수 | `1` | `Pick`의 추첨 횟수입니다. 다른 모드에서는 무시합니다. |
| `Unique` | 불리언 | `true` | `Pick`의 기본 중복 정책입니다. 개별 항목에서 재정의할 수 있습니다. |
| `Entries` | 배열 | 필수 | 비어 있지 않은 보상 항목 목록입니다. |

`OneOf`의 별칭으로 `One`, `Pick`의 별칭으로 `PickN`도 허용하지만 정식 모드 이름을 권장합니다.

| 모드 | 지급 가능한 항목 수 | `Weight` 사용 | 항목별 `Chance` 사용 | `Rolls` / `Unique` 사용 |
| --- | --- | --- | --- | --- |
| `OneOf` | 풀 판정 성공 시 정확히 하나 | 예 | 아니요 | 아니요 |
| `Pick` | 최대 `Rolls`회 추첨 | 예 | 아니요 | 예 |
| `All` | 풀 판정 성공 시 모든 항목을 한 번씩 | 아니요 | 아니요 | 아니요 |
| `Independent` | 0개부터 전체 항목까지 | 아니요 | 예 | 아니요 |

네 모드 모두 풀 자체의 `Chance`를 사용합니다. 하나의 보상 정의에 여러 풀이 있으면 각각 독립적으로 처리하고, 그 결과를 직접 지급하는 `Drops`에 더합니다.

### `OneOf`: 가중치에 따라 하나 선택

`OneOf`는 기본 모드입니다. 풀 자체의 확률 판정이 성공하면 정확히 한 항목을 선택합니다. 항목의 선택 확률은 해당 `Weight`를 모든 항목의 가중치 합으로 나눈 값입니다.

```json
{
    "Pools": [
        {
            "Name": "장비 대박 보상",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

가중치 합은 20입니다. 풀 판정이 성공한 경우 네 항목의 선택 확률은 각각 35%, 35%, 25%, 5%입니다. 풀 자체가 활성화될 확률은 35%이므로 알을 받는 최종 확률은 `35% × 5% = 1.75%`입니다.

- `Weight`를 생략하면 `1`을 사용합니다.
- `Weight`는 `1` 이상의 정수여야 합니다. 가중치를 `0`으로 지정하지 말고 항목을 제거하세요.
- `OneOf`는 항상 한 번만 선택하므로 `Rolls`는 무시되고 경고가 발생합니다.
- 항목별 `Chance`는 무시되고 경고가 발생합니다. 상대적인 선택 확률은 `Weight`로 제어하세요.
- 한 항목만 선택하므로 `Unique`는 실질적인 효과가 없습니다.

### `Pick`: 가중치에 따라 중복 없이 여러 항목 선택

`Pick`은 가중치 추첨을 `Rolls`회 반복합니다. 기본값인 `Unique: true`에서는 선택한 항목을 다음 추첨 전에 제거하여 다시 선택되지 않게 합니다. 매 추첨 후 남은 항목을 기준으로 가중치를 다시 계산합니다.

```json
{
    "Pools": [
        {
            "Name": "서로 다른 보상 두 개 선택",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

서로 다른 항목 두 개를 지급합니다. `Rolls`가 중복 없이 선택 가능한 항목 수보다 크면 남은 항목이 없을 때 추첨을 종료하며, 오류로 처리하지 않습니다.

### `Pick`: 중복 선택 허용

풀의 `Unique`를 `false`로 설정하면 이미 선택한 항목도 다음 추첨에 남습니다. 같은 아이템을 여러 번 받으면 지급 전에 수량을 합칩니다.

```json
{
    "Pools": [
        {
            "Name": "보급품 세 번 추첨",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

세 번 모두 `Money`가 나오거나 탄약이 나올 수도 있고, 서로 섞여 나올 수도 있습니다. 예를 들어 `Money`가 두 번 선택되면 따로 두 번 지급하는 대신 10,000개로 합쳐 한 번 지급합니다.

### `Pick`: 항목별 `Unique` 재정의

항목별 `Unique`는 해당 항목에 대해서만 풀 기본값을 대체합니다. 따라서 같은 풀 안에 반복 가능한 일반 보상과 한 번만 선택되는 대박 보상을 함께 넣을 수 있습니다.

```json
{
    "Pools": [
        {
            "Name": "중복 가능한 화폐와 중복 불가 대박 보상",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

`Money` 항목에는 `Unique: false`가 있으므로 선택 후에도 후보 목록에 남습니다. 갑옷과 투구는 풀의 `Unique: true`를 상속하므로 선택 후 제거됩니다. 반대로 풀에 `Unique: false`를 지정하고 특정 항목에만 `Unique: true`를 지정할 수도 있습니다.

### `All`: 모든 항목 지급

`All`은 풀 자체의 `Chance` 판정이 성공하면 모든 항목을 정확히 한 번씩 지급합니다.

```json
{
    "Pools": [
        {
            "Name": "전체 보상 묶음",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`All`에서는 `Weight`, 항목별 `Chance`, `Unique`가 적용되지 않습니다. `Rolls`는 무시되고 경고가 발생합니다. 묶음 전체를 확률형으로 지급하려면 풀의 `Chance`를 설정하세요. 개별 항목을 확률형으로 지급하려면 `Independent` 또는 직접 지급하는 `Drops`를 사용하세요.

### `Independent`: 각 항목을 별도로 추첨

`Independent`는 모든 항목을 확인하고 각 항목의 `Chance`로 판정합니다. 아무것도 지급하지 않거나, 하나·여러 개·전체 항목을 지급할 수 있습니다.

```json
{
    "Pools": [
        {
            "Name": "독립적인 추가 보상 추첨",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

먼저 풀이 80% 확률로 활성화됩니다. 활성화되면 `Money`는 `Chance`를 생략했으므로 확정 지급됩니다. 나머지 세 항목은 각각 50%, 10%, 5% 확률로 독립적으로 추첨합니다.

- 항목의 `Chance`를 생략하면 `100`을 사용합니다.
- 이 모드에서는 `Weight`와 `Unique`가 적용되지 않습니다.
- 모든 항목을 한 번씩 판정하므로 `Rolls`는 무시되고 경고가 발생합니다.

### 직접 지급 보상과 여러 풀 함께 사용

한 플레이어에게 서로 독립적인 여러 종류의 보상을 지급하려면 여러 풀을 사용하세요.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "장비 한 개",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "보급품 두 번 추첨",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "독립적인 희귀 추가 보상",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

직접 지급하는 `Money`와 경험치는 항상 적용됩니다. 첫 번째 풀은 장비 한 개를 추가하고, 두 번째 풀은 중복을 허용하며 가중치에 따라 보급품을 두 번 추첨합니다. 세 번째 풀은 추가 보상 두 개를 독립적으로 추첨합니다. 풀끼리는 서로 경쟁하지 않으므로 한 플레이어가 모든 풀에서 보상을 받을 수 있습니다.

### 팰 알 보상

알에는 `EggID`와 `PalTemplate`이 모두 필요합니다. 템플릿은 `Pals/Templates/`에서 불러오며 `.json`은 생략할 수 있습니다. `Count`는 지급할 알의 수입니다. `Level: 0`을 사용하거나 레벨을 생략하면 템플릿의 레벨을 유지하고, 양수 고정값 또는 범위를 지정하면 해당 값으로 대체합니다.

```json
{
    "Pools": [
        {
            "Name": "무작위 알 보상 한 개",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

보상 지급 시 알의 템플릿을 가져올 수 없으면 오류를 로그에 기록하고 해당 알 보상을 건너뜁니다.

### 중복 결과 합치기

직접 지급 보상과 모든 풀의 결과는 지급 전에 합칩니다.

- 같은 `ItemID`의 아이템은 수량을 더하여 합칩니다.
- 알은 `EggID`, `PalTemplate`, 추첨된 `Level`이 모두 같을 때만 합칩니다.
- 경험치, 기술 포인트, 고대 기술 포인트는 각각 합산합니다.
- 지급할 아이템 수량과 기술 포인트 총량은 부호 있는 32비트 정수의 최댓값(`2,147,483,647`)으로 제한합니다.

따라서 `Pick`에서 중복 선택된 결과는 보상 요청에 중복 인벤토리 항목을 만들지 않습니다. 추첨된 레벨이 다른 알은 별도 보상으로 유지됩니다.

### `DisableDamageMeter`의 보상 지급 방식

`DisableDamageMeter`가 `true`이면 피해량 순위를 만들지 않고 숫자 순위 보상도 사용하지 않습니다. 대신 소환된 팰에게 피해를 주지 않은 플레이어까지 포함하여 **이벤트 종료 시 접속 중인 모든 플레이어**에 대해 `Rewards.Default`를 각각 추첨합니다.

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

모든 접속 중인 플레이어에게 `Money`를 지급합니다. 선택적으로 지급하는 포인트 보상 두 개는 플레이어마다 따로 추첨합니다. `Default`가 없거나 비어 있으면 이 모드에서는 아무도 보상을 받지 않으며 로그에 경고를 기록합니다.

### 잘못된 조합과 무시되는 설정

보상 데이터가 잘못되면 PalSummon 파일을 불러올 수 없습니다. 알 수 없거나 해당 상황에서 무시되는 필드는 경고를 발생시키므로, 오타나 효과 없는 설정을 PalDefender 로그에서 확인할 수 있습니다.

| 설정 | 결과 |
| --- | --- |
| 한 항목에 `ItemID`와 `EXP`가 모두 있음 | 오류: 항목에는 보상 유형을 하나만 정의할 수 있습니다. |
| 보상 항목에 아이템, 알 또는 성장 보상 필드가 없음 | 오류: 지급할 보상을 판단할 수 없습니다. |
| `Count: 0`, `Weight: 0`, `Rolls: 0` | 오류: 이 값은 `1` 이상이어야 합니다. |
| 범위에 `Min` 또는 `Max`가 없거나 `Max < Min`임 | 오류. |
| `Chance`가 `0`–`100` 범위를 벗어남 | 오류. |
| 풀에 `Entries`가 없거나, 배열이 비어 있거나, 배열이 아닌 값임 | 오류. |
| `OneOf`, `Pick`, `All`의 개별 항목에 `Chance` 지정 | 경고: 항목별 확률을 무시합니다. |
| `OneOf`, `All`, `Independent`에 `Rolls` 지정 | 경고: `Rolls`를 무시합니다. |
| 직접 지급하는 `Drops`에 `Weight` 또는 `Unique` 지정 | 경고: 직접 지급 보상에는 `Chance`를 사용하세요. |
| `Wieght` 같은 알 수 없는 필드가 있음 | 경고: 해당 필드는 사용하지 않습니다. |

주석과 마지막 항목 뒤의 쉼표 없이 올바른 JSON을 작성하세요. 소환 파일을 정상적으로 불러왔더라도 경고를 확인하세요. 경고는 대개 효과 없는 설정을 알려 줍니다.

## 전체 예제

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "투기장 아누비스",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "우승자 추가 보상",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## 검증 체크리스트

1. 먼저 `/givemepal_j <template>`으로 참조하는 템플릿을 테스트하세요.
2. `/getpos`로 `X`, `Y`, `Z`를 확인하세요. RCON에서는 `/getpos`에 UserId를 지정해야 합니다.
3. 주석과 마지막 항목 뒤의 쉼표 없이 올바른 JSON을 작성하세요.
4. 보상 항목마다 보상 유형을 하나만 사용하세요.
5. 각 풀에 비어 있지 않은 `Entries` 배열이 있고, 선택한 `Mode`에 적용되는 필드만 사용하는지 확인하세요.
6. `/summon <filename>`을 실행하고 PalDefender 로그에서 구체적인 검증 오류와 경고를 확인하세요.
