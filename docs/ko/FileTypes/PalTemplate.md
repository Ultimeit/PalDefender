# 📄 `PalTemplate.json`

<https://paldeck.cc/creator>를 이용하면 훨씬 쉽게 파일을 만들 수 있습니다!

!!! tip "ID 조회"
    `PalID`는 [paldeck.cc/pals](https://paldeck.cc/pals), `Passives`는 [paldeck.cc/passives](https://paldeck.cc/passives), `ActiveSkills`와 `LearntSkills`는 [paldeck.cc/skills](https://paldeck.cc/skills)에서 확인하세요.

| 키                       | 자료형 | 설명                                                                                |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | 문자열 | 생성할 팰의 내부 ID입니다. 유효한 [`PalID`](https://paldeck.cc/pals)는 Paldeck에서 확인하세요. |
| `UniqueNPCID`            | 문자열 | NPC 생성에 사용하는 내부 ID입니다. |
| `Nickname`               | 문자열 | 팰에게 붙일 별명입니다. 선택 사항입니다. |
| `SkinId`                 | 문자열 | 팰의 외형을 변경하는 스킨 ID입니다. `/getskinids`로 ID 목록을 조회하세요. |
| `Gender`                 | 문자열 | `"Male"`(수컷), `"Female"`(암컷), `"None"`(없음) 중 하나입니다. |
| `Level`                  | 정수 | 팰의 레벨입니다. |
| `Exp`                    | 정수 | 경험치입니다. |
| `Shiny`                  | 불리언 | 희귀 팰 여부입니다. |
| `PartnerSkillLevel`      | 정수 | 팰의 파트너 스킬 레벨입니다. 반드시 1 이상이어야 합니다! |
| `CondensedPals`          | 정수 | 이 팰에 농축한 팰의 수입니다. |
| `UnusedStatusPoints`     | 정수 | 직접 배분할 수 있는 잔여 능력치 포인트입니다. 플레이어에게만 사용되는 값으로 추정됩니다. |
| `FriendshipPoints`       | 정수 | 팰의 친밀도입니다. |
| `PhysicalHealth`         | 문자열 | 신체 건강 상태입니다. 유효한 이름: `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick`             | 문자열 | 작업 팰의 질병 상태입니다. 유효한 이름: `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter`      | 불리언 | 가져온 캐릭터로 표시합니다. |
| `HP` / `SP` / `MP`       | 숫자 | 기본 체력, 스태미나, 마나입니다. `HP`는 생성된 팰의 최대 체력으로 사용되며, 이 템플릿을 참조하는 PalSummon 및 REST 소환에도 적용됩니다. |
| `Shield`                 | 숫자 | 실드 수치입니다. |
| `Hunger` / `MaxHunger`   | 정수 | 현재 포만도와 최대 포만도입니다. |
| `SAN`                    | 정수 | SAN(팰의 정신적 안정도)입니다. |
| `Support`                | 정수 | AI 행동과 기술에 사용하는 지원 수준입니다. |
| `CraftSpeed`             | 정수 | 제작 속도 배율입니다. |
| `PalSouls`               | 객체 | 팰 영혼 강화 보너스입니다. `Health`, `Attack`, `Defense`, `CraftSpeed`를 포함합니다. 권장되는 일반 범위는 가져오기 규칙에서 제어합니다. |
| `IVs`                    | 객체 | 개체값입니다. `Health`, `AttackMelee`, `AttackShot`, `Defense`를 포함합니다. 권장되는 일반 범위는 가져오기 규칙에서 제어합니다. |
| `ActiveSkills`           | 배열 | 장착한 기술 목록입니다. PalDefender 1.9.0은 관리자 PalTemplate의 항목을 세 개로 줄이지 않으며 모든 항목을 장착 상태로 유지합니다. 유효한 [기술 ID](https://paldeck.cc/skills)는 Paldeck에서 확인하세요. 일반적인 게임/UI 동작은 여전히 기본 슬롯 수를 전제로 할 수 있습니다. |
| `LearntSkills`           | 배열 | 팰이 배웠으며 교체하여 사용할 수 있는 기술입니다. 현재 장착할 기술은 여기에 넣지 마세요. 유효한 [기술 ID](https://paldeck.cc/skills)는 Paldeck에서 확인하세요. |
| `Passives`               | 배열 | 팰의 패시브 특성입니다. 일반 팰은 최대 4개를 사용하세요. 유효한 [`PassiveID`](https://paldeck.cc/passives)는 Paldeck에서 확인하세요. |
| `ExtraWorkSuitabilities` | 객체 | 강화할 작업 적성과 레벨입니다. 예: `"Mining": 2`. 사용 가능한 작업 유형: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |
| `DisableWorkPreferences` | 배열 | 팰이 수행하지 않을 작업 유형입니다. 사용 가능한 작업 유형: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## 작성 지침

1. `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`에 사용자 정의 팰마다 JSON 파일을 하나씩 만드세요.
2. `RaidRewardAnubis.json`처럼 중복되지 않는 파일 이름을 사용하세요. 대부분의 명령어에서 `RaidRewardAnubis` 또는 `RaidRewardAnubis.json`을 사용할 수 있습니다.
3. `PalID`는 반드시 포함하세요. 다른 항목은 선택 사항이며, 생략하면 PalDefender 또는 Palworld 기본값을 사용합니다.
4. `Level`과 `PartnerSkillLevel`은 모두 `1` 이상으로 설정하세요.
5. 장착할 공격 기술은 `ActiveSkills`에, 그 외 배운 기술은 `LearntSkills`에 넣으세요. PalDefender는 이제 초과한 장착 기술을 배운 기술 목록으로 옮기지 않습니다.
6. 팰, 기술, 패시브, 스킨 및 작업 유형의 ID를 정확히 입력하세요. 잘못된 ID는 가져오기에 실패하거나 무시될 수 있습니다.
7. 업로드 전에 JSON 유효성을 검사하세요. JSON에서는 주석과 마지막 항목 뒤의 쉼표를 허용하지 않습니다.
8. 템플릿을 가져올 때 값이 변경되거나 차단되면 서버의 `Pals/ImportRules/Default.json` 및 팰별 예외 설정 파일을 확인하세요.

## 설정 절차

1. 템플릿의 용도를 정하세요. 간단한 관리자 보상, 이벤트 보스, 테스트 팰, 소환용 생성 템플릿 등이 있습니다.
2. [paldeck.cc/pals](https://paldeck.cc/pals)에서 `PalID`를 선택하세요. 표시 이름과 파일 ID가 다를 수 있으므로 ID를 정확히 복사하세요.
3. 직접 설정할 항목만 추가하세요. 짧은 템플릿이 큰 템플릿보다 문제를 찾기 쉽습니다.
4. [paldeck.cc/skills](https://paldeck.cc/skills)에서 기술을 선택하세요. 장착할 공격 기술은 `ActiveSkills`에, 그 외 배운 기술은 `LearntSkills`에 넣으세요.
5. [paldeck.cc/passives](https://paldeck.cc/passives)에서 패시브를 선택하세요. 서버에서 의도적으로 더 많이 허용하는 경우가 아니라면 최대 4개를 사용하세요.
6. 파일을 `Pal/Binaries/Win64/PalDefender/Pals/Templates/`에 저장하세요.
7. 먼저 `/givemepal_j <filename>`으로 테스트하세요. 이후 같은 템플릿을 `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, REST API 또는 `PalSummon.json`에 사용할 수 있습니다.

## 예제 설명

아래 최소 예제는 공격 기술 세 개와 패시브 두 개를 가진 레벨 50 아누비스를 생성합니다. 필수 항목인 `PalID`와 자주 쓰는 항목 몇 개만 있어 테스트에 적합합니다.

큰 예제는 의도적으로 극단적인 값을 사용하며, 영혼 강화, 개체값, 기술, 패시브, 작업 적성 재정의에 사용할 수 있는 구조를 보여 줍니다. 가져오기 규칙을 사용하는 서버에서는 높은 값이 상한으로 조정되거나 차단될 수 있습니다.

## 최소 예제

```json
{
    "PalID": "Anubis",
    "Nickname": "투기장 아누비스",
    "Gender": "None",
    "Level": 50,
    "PartnerSkillLevel": 1,
    "HP": 3500,
    "SAN": 100,
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "RockLance"
    ],
    "Passives": [
        "Legend",
        "CraftSpeed_up3"
    ]
}
```

## 예제

파일을 다음 위치에 저장하세요: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate`은 폴더 안에서 중복되지 않는 이름이면 됩니다. 이 이름을 `/givepal_j`와 `/spawnpal_j`의 인수로 사용합니다!)

```json
{
    "PalID": "Anubis",
    "Nickname": "최강 아누비스",
    "Gender": "None",
    "Level": 255,
    "Shiny": true,
    "PartnerSkillLevel": 255,
    "HP": 999999,
    "SP": 999999,
    "MP": 999999,
    "Hunger": 999999,
    "MaxHunger": 999999,
    "SAN": 999999,
    "Support": 999999,
    "CraftSpeed": 999999,
    "PalSouls": {
        "Health": 255,
        "Attack": 255,
        "Defense": 255,
        "CraftSpeed": 255
    },
    "IVs": {
        "Health": 255,
        "AttackMelee": 255,
        "AttackShot": 255,
        "Defense": 255
    },
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "Unique_Anubis_LowRoundKick"
    ],
    "Passives": [
        "Legend",
        "PAL_ALLAttack_up3",
        "Deffence_up3",
        "Vampire",
        "Stamina_Up_3",
        "EternalFlame",
        "PAL_Sanity_Down_3",
        "Invader",
        "SwimSpeed_up_3",
        "Rare",
        "Nushi",
        "PAL_FullStomach_Down_3",
        "CraftSpeed_up3",
        "Salvation",
        "Witch",
        "MoveSpeed_up_3",
        "SwimSpeed_up_2",
        "CraftSpeed_up2",
        "Deffence_up2",
        "ElementBoost_Normal_2_PAL",
        "PAL_FullStomach_Down_2",
        "ElementBoost_Dragon_2_PAL",
        "ElementBoost_Earth_2_PAL",
        "PAL_ALLAttack_up2",
        "ElementBoost_Fire_2_PAL",
        "ElementBoost_Ice_2_PAL",
        "Stamina_Up_1",
        "TrainerLogging_up1",
        "ElementBoost_Thunder_2_PAL",
        "ElementBoost_Aqua_2_PAL",
        "ElementBoost_Dark_2_PAL",
        "TrainerMining_up1",
        "TrainerWorkSpeed_UP_1",
        "SalePrice_Up_1",
        "Test_PalEgg_HatchingSpeed_Up",
        "MoveSpeed_up_2",
        "CoolTimeReduction_Up_1",
        "ElementBoost_Leaf_2_PAL",
        "TrainerDEF_UP_1",
        "TrainerATK_UP_1",
        "PAL_Sanity_Down_2",
        "ElementResist_Normal_1_PAL",
        "ElementBoost_Dragon_1_PAL",
        "ElementResist_Leaf_1_PAL",
        "PAL_ALLAttack_up1",
        "ElementBoost_Thunder_1_PAL",
        "ElementResist_Dark_1_PAL",
        "ElementBoost_Ice_1_PAL",
        "PAL_FullStomach_Down_1",
        "ElementResist_Dragon_1_PAL",
        "ElementResist_Earth_1_PAL",
        "SalePrice_Up_2",
        "Stamina_Up_2",
        "ElementBoost_Leaf_1_PAL",
        "Deffence_up1",
        "ElementResist_Ice_1_PAL",
        "ElementBoost_Aqua_1_PAL",
        "CoolTimeReduction_Up_2",
        "ElementResist_Thunder_1_PAL",
        "MoveSpeed_up_1",
        "Alien",
        "PAL_Sanity_Down_1",
        "ElementBoost_Earth_1_PAL",
        "ElementBoost_Fire_1_PAL",
        "CraftSpeed_up1",
        "SwimSpeed_up_1",
        "ElementResist_Fire_1_PAL",
        "ElementBoost_Dark_1_PAL",
        "ElementResist_Aqua_1_PAL",
        "ElementBoost_Normal_1_PAL"
    ],
    "ExtraWorkSuitabilities": {
        "EmitFlame": 5,
        "Watering": 5,
        "Seeding": 5,
        "GenerateElectricity": 5,
        "Handcraft": 5,
        "Collection": 5,
        "Deforest": 5,
        "Mining": 5,
        "OilExtraction": 5,
        "ProductMedicine": 5,
        "Cool": 5,
        "Transport": 5,
        "MonsterFarm": 5,
        "Anyone": 5
    }
}
```
