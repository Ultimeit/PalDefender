# POST /give/progression/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/give/progression/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Progression.Give`

## 용도

플레이어에게 성장 관련 수치를 지급합니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

지원되는 지급 항목을 하나 이상 포함하는 JSON 객체입니다. 양의 정수 `EXP`, `TechnologyPoints`, `AncientTechnologyPoints` 또는 유물 유형을 키로 하고 양의 정수를 값으로 하는 비어 있지 않은 `Relics` 객체를 지정하세요.


지원되는 유물 유형: `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/give-progression.md"

## 오류 응답

오류 응답 본문은 다음 형식을 사용합니다:

```json
{
    "Error": {
        "Code": "ERROR_CODE",
        "Message": "사람이 읽을 수 있는 오류 메시지",
        "Details": {}
    }
}
```

| HTTP | 오류 코드 | 발생 조건 |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` 헤더가 없거나 형식이 잘못되었거나, 설정된 Bearer 토큰과 일치하지 않습니다. |
| `403` | `MISSING_PERMISSION` | 토큰은 유효하지만 이 엔드포인트에 필요한 권한이 없습니다. |
| `400` | `INVALID_JSON` | 요청 본문이 있지만 JSON으로 해석할 수 없습니다. |
| `400` | `REQUEST_FAILED` | 게임 스레드 콜백에서 예외가 발생했거나 공통 플레이어/리소스 확인 처리에 실패했습니다. |
| `500` | `REQUEST_TIMEOUT` | 내부 게임 스레드 콜백이 5초 안에 완료되지 않았습니다. |
| `400` | `INVALID_REQUEST` | 본문에 `EXP`, `Relics`, `TechnologyPoints`, `AncientTechnologyPoints` 중 어느 항목도 없습니다. |
| `400` | `VALIDATION_FAILED` | 지정한 성장 값이 없거나 정수가 아니거나 0 이하이거나, 필요한 내부 성장 데이터에 접근할 수 없습니다. |

## 예제

### GDK 플레이어에게 경험치 지급

```http
POST /v1/pdapi/give/progression/gdk_2533274898765432
```

```json
{
    "EXP": 25000
}
```

### PlayerUID로 포인트와 유물 지급

```http
POST /v1/pdapi/give/progression/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

```json
{
    "Relics": {
        "CapturePower": 5,
        "MoveSpeed": 2
    },
    "TechnologyPoints": 10,
    "AncientTechnologyPoints": 2
}
```

## 활용 사례

- 저장 데이터 롤백 후 플레이어에게 보상합니다.
- 특정 기술을 해금하지 않고 기술 포인트를 추가합니다.
- 특정 [`TechID`](https://paldeck.cc/technology)를 해금하려면 [POST /learntech](learntech.md)를 사용하세요.
