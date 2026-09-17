# 📄 `Pals/ImportRules/*.json`


팰 가져오기 규칙은 명령어나 API로 `PalTemplate.json`을 가져올 때 허용, 차단 또는 값 조정 여부를 제어합니다.

!!! tip "ID 조회"
    `AllowedPalIDs`, `BannedPalIDs` 및 팰별 규칙 파일 이름에 사용할 ID는 [paldeck.cc/pals](https://paldeck.cc/pals)에서, `DisallowedPassives`에 사용할 ID는 [paldeck.cc/passives](https://paldeck.cc/passives)에서 확인하세요.

## 파일 위치

| 파일 | 용도 |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | 모든 팰 템플릿에 적용되는 공통 가져오기 규칙입니다. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | 선택적으로 사용하는 팰별 예외 설정입니다. Paldeck에서 [`PalID`](https://paldeck.cc/pals)를 찾아 정확히 같은 ID를 파일 이름으로 사용하세요. 예: `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | 참고용으로 생성되는 예제 파일입니다. 복사하여 이름을 변경해야 실제 팰 규칙으로 적용됩니다. |

## 설정 키

| 키 | 자료형 | 설명 |
| --- | ---- | ----------- |
| `PalSelectionMode` | 문자열 | `Default.json` 전용입니다. `AllowAllExceptBanned`는 `BannedPalIDs`를 제외한 모든 팰을 허용합니다. `AllowOnlyListed`는 `AllowedPalIDs`에 있는 팰만 허용합니다. |
| `AllowedPalIDs` | 배열 | `Default.json` 전용입니다. `PalSelectionMode`가 `AllowOnlyListed`일 때 허용되는 [`PalID`](https://paldeck.cc/pals) 목록입니다. |
| `BannedPalIDs` | 배열 | `Default.json` 전용입니다. 항상 차단되는 [`PalID`](https://paldeck.cc/pals) 목록입니다. |
| `MaxValueLimitAction` | 문자열 | `BlockImport`는 설정된 상한을 넘는 템플릿을 차단합니다. `ClampToMaxValues`는 값을 설정된 상한으로 낮춥니다. |
| `DisallowedPassivesAction` | 문자열 | `BlockImport`는 목록에 있는 패시브를 가진 템플릿을 차단합니다. `RemoveFromPal`은 가져오기 전에 해당 패시브를 제거합니다. |
| `DisallowedPassives` | 배열 | `DisallowedPassivesAction`의 적용 대상인 [`PassiveID`](https://paldeck.cc/passives) 목록입니다. |
| `ConditionMode` | 문자열 | `None`은 추가 조건 없이 규칙을 적용합니다. `RequirePalCaptureCount`는 플레이어가 같은 종의 팰을 지정된 횟수 이상 포획한 경우에만 가져오기를 허용합니다. |
| `RequiredCaptureCount` | 정수 | `ConditionMode`가 `RequirePalCaptureCount`일 때 필요한 같은 종의 포획 횟수입니다. 기본값은 `5`입니다. |
| `Disabled` | 불리언 | `true`이면 해당 규칙 집합의 가져오기 검사를 끕니다. |
| `BanIfPalIsImpossible` | 불리언 | `true`이면 불가능한 팰을 가져오려는 시도에 서버 설정에 따른 제재를 적용할 수 있습니다. |
| `AllowGenderNone` | 불리언 | `false`이면 `Gender: "None"`인 템플릿이 가져오기 검사에서 거부될 수 있습니다. |
| `MaxLevel` | 정수 | 가져오는 템플릿에 허용되는 팰 레벨 상한입니다. |
| `MaxRank` | 정수 | 가져오는 템플릿에 허용되는 파트너 스킬 등급 상한입니다. |
| `PalSouls` | 객체 | 팰 영혼 강화 수치의 상한입니다: `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | 객체 | 개체값(IV)의 상한입니다: `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## 작성 지침

1. 먼저 `Default.json`에서 서버 전체에 적용할 정책을 설정하세요.
2. 특정 팰에 다른 제한이 필요한 경우에만 팰별 파일을 사용하세요.
3. 팰별 파일 이름은 `Anubis.json`처럼 팰 ID와 일치해야 합니다.
4. `PalSelectionMode`, `AllowedPalIDs`, `BannedPalIDs`는 팰별 파일에 넣지 마세요. `Default.json`에만 지정합니다.
5. 엄격하게 제한하려면 `BlockImport`를 사용하세요.
6. 템플릿을 허용하되 상한을 넘는 값만 낮추려면 `ClampToMaxValues`를 사용하세요.
7. 가져오기를 실패시키는 대신 금지된 패시브를 자동으로 제거하려면 `RemoveFromPal`을 사용하세요.
8. ID를 정확히 입력하고 업로드 전에 JSON 유효성을 검사하세요.

## 설정 절차

1. `Pals/ImportRules/Default.json`을 열거나 새로 만드세요.
2. 전체 팰 허용 정책을 정하세요.
   - 대부분의 팰을 허용하고 일부만 차단하려면 `AllowAllExceptBanned`를 사용하세요.
   - 승인된 목록의 팰만 가져오게 하려면 `AllowOnlyListed`를 사용하세요.
3. 제한 처리 방식을 정하세요.
   - 잘못된 템플릿을 거부하는 엄격한 서버에서는 `BlockImport`를 사용하세요.
   - 템플릿을 허용하되 상한을 넘는 레벨, 등급, 영혼 강화 수치, 개체값만 낮추려면 `ClampToMaxValues`를 사용하세요.
   - 템플릿 전체를 거부하는 대신 원치 않는 패시브만 제거하려면 `RemoveFromPal`을 사용하세요.
4. [paldeck.cc/passives](https://paldeck.cc/passives)에서 금지할 패시브를 찾아 추가하세요.
5. [paldeck.cc/pals](https://paldeck.cc/pals)에서 차단하거나 허용할 팰을 찾아 추가하세요.
6. 특정 팰에 공통 설정보다 엄격하거나 느슨한 제한이 필요한 경우에만 팰별 예외 설정을 추가하세요.
7. 큰 템플릿을 가져오기 전에 간단한 `PalTemplate.json`으로 먼저 테스트하세요.

## 자주 사용하는 설정

### 대부분의 팰을 허용하고 일부만 차단

일반적인 관리자 보상은 허용하되 특정 팰은 가져오지 못하게 하려는 경우에 사용하세요.

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "BannedPalIDs": [
        "JetDragon",
        "BOSS_Anubis"
    ],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

### 승인된 목록만 허용

플레이어가 가져오는 템플릿을 승인된 팰로 제한하려는 경우에 사용하세요.

```json
{
    "PalSelectionMode": "AllowOnlyListed",
    "AllowedPalIDs": [
        "Anubis",
        "Kirin",
        "WeaselDragon"
    ],
    "BannedPalIDs": [],
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 50,
    "MaxRank": 4,
    "PalSouls": {
        "Health": 10,
        "Attack": 10,
        "Defense": 10,
        "CraftSpeed": 10
    },
    "IVs": {
        "Health": 80,
        "AttackMelee": 80,
        "AttackShot": 80,
        "Defense": 80
    }
}
```

이 설정에서는 목록에 있는 세 가지 `PalID`만 가져올 수 있습니다. 상한을 넘는 값은 설정된 최댓값으로 낮아지고, 목록에 있는 패시브는 팰에서 제거됩니다.

## 기본 설정 예제

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "BannedPalIDs": [
        "JetDragon"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

## 팰별 예외 설정 예제

### `Anubis.json`
```json
{
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "AllowGenderNone": false,
    "MaxLevel": 10,
    "MaxRank": 3,
    "PalSouls": {
        "Health": 5,
        "Attack": 5,
        "Defense": 5,
        "CraftSpeed": 5
    },
    "IVs": {
        "Health": 50,
        "AttackMelee": 50,
        "AttackShot": 50,
        "Defense": 50
    }
}
```
