# GET /items/{player_identifier}



**엔드포인트:** `GET /v1/pdapi/items/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Items.Read`

## 용도

대상 플레이어의 아이템 목록을 조회합니다. 응답에 있는 아이템 식별자는 [paldeck.cc/items](https://paldeck.cc/items)에서 검색할 수 있습니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/items.md"

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
| `400` | `REQUEST_FAILED` | 대상 플레이어, 플레이어 상태, 인벤토리 데이터 또는 일반 인벤토리 컨테이너를 확인할 수 없습니다. |
| `500` | `REQUEST_TIMEOUT` | 내부 게임 스레드 콜백이 5초 안에 완료되지 않았습니다. |

## 예제

### Steam 플레이어의 인벤토리 조회

```http
GET /v1/pdapi/items/steam_76561198087654321
```

### GDK 플레이어의 인벤토리 조회

```http
GET /v1/pdapi/items/gdk_2533274812345678
```

## 활용 사례

- 보상을 지급하기 전에 인벤토리를 확인합니다.
- [POST /give/items](give-items.md)를 사용하기 전에 [`ItemID`](https://paldeck.cc/items)를 확인하세요.
- 아이템 분실 제보의 원인을 확인합니다.
