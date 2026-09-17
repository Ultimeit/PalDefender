# GET /progression/{player_identifier}



**엔드포인트:** `GET /v1/pdapi/progression/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Progression.Read`

## 용도

경험치, 레벨 관련 상태, 유물 총량, 기술 포인트 총량 등 플레이어의 성장 정보를 조회합니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/progression.md"

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
| `400` | `REQUEST_FAILED` | 대상 플레이어, 계정, 개별 캐릭터 데이터, 기록 데이터 또는 기술 데이터를 확인할 수 없습니다. |
| `500` | `REQUEST_TIMEOUT` | 내부 게임 스레드 콜백이 5초 안에 완료되지 않았습니다. |

## 예제

### PS5 UserID로 성장 정보 조회

```http
GET /v1/pdapi/progression/ps5_c481a77e22004b9d
```

### PlayerUID로 성장 정보 조회

```http
GET /v1/pdapi/progression/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## 활용 사례

- 성장 보상을 지급하기 전에 현재 값을 확인합니다.
- [POST /give/progression](give-progression.md)으로 지원 작업을 수행한 뒤 결과를 확인합니다.
- 신뢰할 수 있는 관리자 대시보드에 플레이어 요약 패널을 만듭니다.
