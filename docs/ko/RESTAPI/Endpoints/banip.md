# POST /banip/{ip}



**엔드포인트:** `POST /v1/pdapi/banip/<ip>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Punishments.BanIP`

## 용도

IP 주소를 차단하고 `Banlist.json`에 기록합니다.

## 경로 매개변수

- `ip`: 차단할 IP 주소입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

선택 JSON 필드는 문자열 `Reason`과 `UserId`입니다. IP 차단을 사용자와 연결하려면 `UserId`를 지정하세요.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/banip.md"

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

## 예제

### IP 주소만 차단

```http
POST /v1/pdapi/banip/203.0.113.42
```

```json
{
    "Reason": "봇 트래픽"
}
```

### IP 주소를 차단하고 GDK 사용자 연결

```http
POST /v1/pdapi/banip/198.51.100.87
```

```json
{
    "Reason": "부계정 악용",
    "UserId": "gdk_2533274898765432"
}
```

## 활용 사례

- 운영진 검토 후 같은 IP에서 반복되는 악용을 차단합니다.
- 사용자 ID를 알고 있다면 `UserId`를 연결하여 차단 기록을 쉽게 검토할 수 있도록 하세요.
- [GET /banlist](banlist.md)의 `ip` 필터로 활성 차단 기록을 확인하세요.
