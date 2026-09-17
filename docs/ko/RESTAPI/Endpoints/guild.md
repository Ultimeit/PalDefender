# GET /guild/{guild_id}



**엔드포인트:** `GET /v1/pdapi/guild/<guild_id>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Guild.Read`

## 용도

길드 하나의 상세 멤버 및 거점 정보를 반환합니다.

## 경로 매개변수

- `guild_id`: 길드 식별자입니다. 보통 [GET /guilds](guilds.md)에서 복사합니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/guild.md"

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
| `404` | `GUILD_NOT_FOUND` | 지정한 `guild_id`와 일치하는 길드가 없습니다. |

## 예제

### 길드 멤버와 거점 조회

```http
GET /v1/pdapi/guild/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

### GUID로 다른 길드 조회

```http
GET /v1/pdapi/guild/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

## 활용 사례

- 거점을 삭제하기 전에 소유권을 확인합니다.
- 지원 요청에 대응하기 위해 길드 멤버와 거점 데이터를 검토합니다.
- 응답의 거점 ID를 [POST /deletebase](deletebase.md)에 사용할 때는 주의하세요.
