# POST /ban/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/ban/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Punishments.Ban`

## 용도

사용자를 차단하고 `Banlist.json`에 기록합니다. 대상이 접속 중이면 강제 퇴장될 수 있습니다.

## 경로 매개변수

- `player_identifier`: `UserId`, `PlayerUID` 또는 지원되는 다른 플레이어 식별자입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

선택 JSON 필드는 문자열 `Reason`과 불리언 `IP`입니다. 확인된 IP 주소도 함께 차단하려는 경우에만 `IP`를 `true`로 설정하세요.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/ban.md"

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
| `400` | `IP_UNAVAILABLE` | `IP`가 `true`이지만 대상 사용자의 IP 주소를 확인할 수 없습니다. |

## 예제

### Steam 사용자 차단

```http
POST /v1/pdapi/ban/steam_76561198012345678
```

```json
{
    "Reason": "결제 취소 사기"
}
```

### PS5 사용자와 확인된 IP 주소 차단

```http
POST /v1/pdapi/ban/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Reason": "차단 회피",
    "IP": true
}
```

## 활용 사례

- 운영진 검토 후 `UserId`로 플레이어를 차단합니다.
- 다른 운영진이 나중에 차단 기록을 이해할 수 있도록 명확한 사유를 적으세요.
- [GET /banlist](banlist.md)로 활성 차단 기록을 확인하세요. 차단 데이터는 더 이상 `Config.json`에서 관리하지 않습니다.
