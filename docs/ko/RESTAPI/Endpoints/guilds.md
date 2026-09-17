# GET /guilds



**엔드포인트:** `GET /v1/pdapi/guilds`

**인증:** Bearer 토큰

**필요 권한:** `REST.Guilds.Read`

## 용도

서버가 알고 있는 길드의 요약 정보를 나열합니다. 특정 길드를 조회하기 전에 이 엔드포인트로 길드 ID를 확인하세요.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/guilds.md"

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

## 예제

### 모든 길드 조회

```http
GET /v1/pdapi/guilds
```

### 길드 대시보드 데이터 갱신

```http
GET /v1/pdapi/guilds
```

## 활용 사례

- 관리자 패널에 길드 선택 기능을 만듭니다.
- [GET /guild](guild.md)에 사용할 `guild_id`를 찾습니다.
- 거점 수, 멤버 수, 길드 소유권을 한눈에 검토합니다.
