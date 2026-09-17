# GET /players



**엔드포인트:** `GET /v1/pdapi/players`

**인증:** Bearer 토큰

**필요 권한:** `REST.Players.Read`

## 용도

서버가 알고 있는 플레이어의 식별 정보와 상태를 나열합니다. 관리자 도구의 플레이어 선택 기능에 사용하세요.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/players.md"

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
| `500` | `PLAYER_MANAGER_UNAVAILABLE` | 서버에서 Palworld 플레이어 관리자에 접근할 수 없습니다. |

## 예제

### 서버가 알고 있는 모든 플레이어 조회

```http
GET /v1/pdapi/players
```

### 관리자용 플레이어 선택 목록 갱신

```http
GET /v1/pdapi/players
```

## 활용 사례

- 접속 중인 플레이어와 서버에 등록된 플레이어의 드롭다운 목록을 만듭니다.
- 보상, 제재 또는 인벤토리 엔드포인트를 호출하기 전에 정확한 `UserId`나 `PlayerUID`를 찾습니다.
- 메시지나 점검 예고를 보내기 전에 접속자를 확인합니다.

## 관련 문서

- 플레이어 한 명을 조회하려면 [GET /player](player.md)를 사용하세요.
- [POST /kick](kick.md), [POST /ban](ban.md) 및 보상 엔드포인트도 같은 형식의 플레이어 식별자를 사용합니다.
