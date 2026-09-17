# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>사용 중단</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>사용 중단</span> 기존 엔드포인트"
    이 기존 보상 엔드포인트는 사용이 중단되었습니다. 기능별 엔드포인트인 [성장 보상 지급](./give-progression.md), [아이템 지급](./give-items.md), [팰 지급](./give-pals.md), [팰 템플릿 지급](./give-paltemplate.md), [팰 알 지급](./give-paleggs.md)을 사용하세요.


## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/give_deprecated.md"

## 오류 응답

이 엔드포인트는 사용이 중단되었으며 현재 빌드에 없을 수 있습니다. 제공되는 경우 오류 본문은 현재 API와 같은 공통 REST 오류 형식을 사용합니다.

| HTTP | 오류 코드 | 발생 조건 |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | `Authorization` 헤더가 없거나 형식이 잘못되었거나, 설정된 Bearer 토큰과 일치하지 않습니다. |
| `403` | `MISSING_PERMISSION` | 토큰은 유효하지만 이 사용 중단 경로에 필요한 권한이 없습니다. |
| `400` | `INVALID_JSON` | 요청 본문이 있지만 JSON으로 해석할 수 없습니다. |
| `400` | `REQUEST_FAILED` | 기존 보상 작업에서 요청을 검증하거나 적용하는 중 실패했습니다. |
| `500` | `REQUEST_TIMEOUT` | 내부 게임 스레드 콜백이 5초 안에 완료되지 않았습니다. |

## 예제

### 경험치와 아이템 지급

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### 팰과 알 지급

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

??? info "POST `/v1/pdapi/give` — 경험치 / 아이템 / 팰 / 알 일괄 지급(원자적 처리)"
    ## POST `/v1/pdapi/give`
    ### 기능
    서버 측에서 트랜잭션과 유사한 하나의 작업으로 대상 플레이어에게 보상을 지급합니다:

    - 경험치 및/또는
    - 아이템 및/또는
    - 팰 및/또는
    - 알
    지급할 보상은 요청 본문에 따라 결정됩니다.

    ### 핵심 동작
    이 엔드포인트는 **원자적 처리**를 목표로 합니다:

    - 모든 보상을 지급하거나
    - 아무것도 지급하지 않습니다.

    입력 오류, 인벤토리 공간 부족, 잘못된 ID 등으로 일부 작업이 실패하면 서버는 요청 전체를 거부해야 하며, 일부만 적용해서는 안 됩니다.

    ### 이 동작이 필요한 이유
    관리자 도구가 실수로 다음 상태를 만들어서는 안 됩니다:

    - 경험치만 지급하고 아이템은 지급하지 않는 상태
    - 일부 아이템만 지급한 뒤 나머지 지급에 실패하는 상태
    - 팰만 생성하고 아이템은 지급하지 않는 상태

    원자적 처리는 데이터가 어중간하게 적용되는 상황과 복잡한 지원 요청을 방지합니다.

    ### 지급 가능한 보상
    구현에 따라 요청에 다음 항목을 포함할 수 있습니다:

    - `EXP` — 경험치 추가
    - `Relics` — 유물 유형별 포인트 추가
    - `TechnologyPoints` — 기술 포인트 추가
    - `AncientTechnologyPoints` — 고대 기술 포인트 추가
    - `UnlockTechnology` / `Techs[]` — 기술 습득
    - `Items[]` — 수량을 지정하여 아이템 하나 또는 여러 개 지급
    - `Pals[]` — ID와 레벨로 팰 지급
    - `PalTemplates[]` — 파일 이름으로 팰 템플릿 가져오기
    - `PalEggs[]` — 알 ID와 팰 ID / 템플릿으로 알 지급. 레벨 지정 가능


    ### 오류 응답

    이 엔드포인트는 사용이 중단되었으며 현재 빌드에 없을 수 있습니다. 제공되는 경우 현재 API와 같은 공통 REST 오류 형식을 사용합니다. Bearer 인증 실패 시 `INVALID_TOKEN`(`401`), 토큰 인증은 성공했지만 호출 권한이 없으면 `MISSING_PERMISSION`(`403`)을 반환합니다. 요청 검증 실패는 JSON 오류 객체로 반환합니다. 엔드포인트별 오류 코드를 사용하려면 기능별 보상 엔드포인트로 이전하세요.

    ### 예제

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### 검증 및 자주 발생하는 실패
    관리자가 자주 마주치는 오류 원인:

    - 인벤토리 공간: 모든 아이템을 넣을 공간이 부족함 → 요청 전체 실패
    - 잘못된 ID: 알 수 없는 `ItemID`, `PalID`, `EggID` 또는 없는 템플릿 파일 → 실패
    - 잘못된 값:
        - 음수 또는 0인 수량(규칙에 따라 다름)
        - 잘못된 레벨(너무 낮거나 높거나 숫자가 아님)
        - 필수 필드 누락(예: `UserID` 없음)
    - 플레이어를 찾거나 불러올 수 없음:
        - 등록되지 않은 사용자 ID
        - 현재 접속 중이 아닌 플레이어(서버의 오프라인 지급 처리 방식에 따라 다름)

    ### 반환값
    오류 개수와 오류 메시지를 반환합니다. 상태 코드가 200이 아니면 `Errors`에서 오류 개수를 확인하세요. `Error`에는 실패한 항목의 상세 목록이 들어 있습니다.
