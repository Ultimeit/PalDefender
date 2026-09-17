# GET /pals/{player_identifier}



**엔드포인트:** `GET /v1/pdapi/pals/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Pals.Read`

## 용도

대상 플레이어의 팰 목록을 조회합니다. 응답에 있는 팰 식별자는 [paldeck.cc/pals](https://paldeck.cc/pals)에서 검색할 수 있습니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/pals.md"

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
| `404` | `PLAYER_NOT_FOUND` | 지정한 `player_identifier`와 일치하는 접속 중인 플레이어가 없습니다. |
| `404` | `PLAYER_STATE_NOT_FOUND` | 플레이어는 존재하지만 `APalPlayerState`에 접근할 수 없습니다. |

## 예제

### PS5 플레이어의 팰 조회

```http
GET /v1/pdapi/pals/ps5_0f4b8c2d91aa34ef
```

### PlayerUID로 팰 조회

```http
GET /v1/pdapi/pals/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

## 활용 사례

- 지원 작업 전에 플레이어 정보를 검토합니다.
- [POST /give/pals](give-pals.md) 또는 [POST /give/paltemplate](give-paltemplate.md) 사용 후 보상 팰이 지급되었는지 확인합니다.
- 팰 분실이나 예상하지 못한 팰에 대한 제보를 조사합니다.
