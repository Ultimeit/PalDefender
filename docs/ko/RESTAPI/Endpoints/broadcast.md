# POST /Broadcast



**엔드포인트:** `POST /v1/pdapi/Broadcast`

**인증:** Bearer 토큰

**필요 권한:** `REST.Messages.Broadcast`

## 용도

서버 전체에 채팅 메시지를 전송합니다.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

필수 문자열 `Message`를 포함하는 JSON 객체입니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/broadcast.md"

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
| `400` | `VALIDATION_FAILED` | `Message`가 없거나 비어 있거나 문자열이 아닙니다. |

## 예제

### 재시작 예고 전체 공지

```http
POST /v1/pdapi/Broadcast
```

```json
{
    "Message": "15분 후 서버를 재시작합니다."
}
```

## 활용 사례

- 예정된 점검을 공지합니다.
- 이벤트 시작 메시지를 자동으로 전송합니다.
- 일반 전체 채팅 대신 화면 알림이 필요하면 [POST /Alert](alert.md)를 사용하세요.
