# GET /player/{player_identifier}



**엔드포인트:** `GET /v1/pdapi/player/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Player.Read`

## 용도

플레이어 한 명의 정보를 반환합니다. `UserId`, `PlayerUID` 등 지원되는 플레이어 식별자를 사용할 수 있습니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/player.md"

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
| `404` | `PLAYER_ACCOUNT_NOT_FOUND` | 플레이어를 찾았지만 계정 데이터를 불러올 수 없습니다. |

## 예제

### Steam UserID로 조회

```http
GET /v1/pdapi/player/steam_76561198012345678
```

### PlayerUID로 조회

```http
GET /v1/pdapi/player/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

## 활용 사례

- `GET /players`의 목록에서 항목을 선택하여 플레이어 상세 페이지를 엽니다.
- 보상 지급이나 제재 적용 전에 대상을 확인합니다.
- 서버가 현재 해당 플레이어를 찾을 수 있는지 확인합니다.
