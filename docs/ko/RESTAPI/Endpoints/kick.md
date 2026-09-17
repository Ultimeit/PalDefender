# POST /kick/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/kick/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Punishments.Kick`

## 용도

차단 기록을 만들지 않고 접속 중인 플레이어를 강제 퇴장시킵니다.

## 경로 매개변수

- `player_identifier`: `UserId`, `PlayerUID` 또는 지원되는 다른 플레이어 식별자입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

선택 JSON 필드로 문자열 `Reason`을 지정할 수 있습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/kick.md"

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
| `404` | `PLAYER_NOT_FOUND` | 대상 플레이어가 접속 중이 아니거나 찾을 수 없습니다. |

## 예제

### 사유를 지정하여 GDK 플레이어 강제 퇴장

```http
POST /v1/pdapi/kick/gdk_2533274812345678
```

```json
{
    "Reason": "이벤트 구역에서 장시간 자리 비움"
}
```

### 기본 사유로 Steam 플레이어 강제 퇴장

```http
POST /v1/pdapi/kick/steam_76561198087654321
```

```json
{}
```

## 활용 사례

- 점검 전에 플레이어를 퇴장시킵니다.
- 움직일 수 없는 상태의 플레이어를 퇴장시켜 다시 접속할 수 있게 합니다.
- 플레이어의 재접속도 막으려면 [POST /ban](ban.md)을 사용하세요.
