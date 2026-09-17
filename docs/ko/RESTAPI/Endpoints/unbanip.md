# POST /unbanip/{ip}



**엔드포인트:** `POST /v1/pdapi/unbanip/<ip>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Punishments.UnbanIP`

## 용도

`Banlist.json`에서 IP 주소의 차단을 해제합니다.

## 경로 매개변수

- `ip`: 차단을 해제할 IP 주소입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

선택 JSON 필드로 문자열 `Reason`을 지정할 수 있습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/unbanip.md"

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
| `400` | `VALIDATION_FAILED` | 선택 요청 필드의 JSON 자료형이 잘못되었습니다. |
| `404` | `BAN_NOT_FOUND` | 지정한 `ip`에 활성 차단이 없습니다. |

## 예제

### 사유를 지정하여 IP 차단 해제

```http
POST /v1/pdapi/unbanip/203.0.113.42
```

```json
{
    "Reason": "임시 차단 기간 만료"
}
```

### 기본 사유로 IP 차단 해제

```http
POST /v1/pdapi/unbanip/198.51.100.87
```

```json
{}
```

## 활용 사례

- 조사 후 IP 차단을 해제합니다.
- 계정 차단을 해제했지만 IP 차단 기록이 활성 상태로 남아 접속할 수 없는 경우에 사용합니다.
- [GET /banlist](banlist.md)의 `ip`로 결과를 확인하세요.
