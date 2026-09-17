# POST /give/items/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/give/items/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Items.Give`

## 용도

대상 플레이어에게 아이템 하나 또는 여러 개를 지급합니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

아이템 지급 배열인 `Items`를 포함하는 JSON 객체입니다. 각 항목에 [`ItemID`](https://paldeck.cc/items)와 양수 `Count`가 필요합니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/give-items.md"

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
| `400` | `INVALID_REQUEST` | 본문에 `Items` 배열이 없습니다. |
| `400` | `VALIDATION_FAILED` | 지급할 아이템 중 하나 이상이 잘못되었거나 지원되지 않거나, 수량이 너무 많거나 인벤토리에 공간이 부족합니다. |
| `500` | `GRANT_FAILED` | 검증은 통과했지만 서버에서 인벤토리에 아이템을 추가하는 중 실패했습니다. |

## 예제

### Steam 플레이어에게 탄약과 발사기 지급

```http
POST /v1/pdapi/give/items/steam_76561198012345678
```

```json
{
    "Items": [
        { "ItemID": "ExplosiveBullet", "Count": 500 },
        { "ItemID": "Launcher_Default_5", "Count": 1 }
    ]
}
```

### PS5 플레이어에게 화폐 지급

```http
POST /v1/pdapi/give/items/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

## 활용 사례

- 롤백 후 보상 지급에 사용합니다.
- 신뢰할 수 있는 서비스가 구매한 아이템을 지급하는 상점 연동에 사용합니다.
- 먼저 [`ItemID`](https://paldeck.cc/items)를 확인하세요. 표시 이름이 항상 유효한 ID인 것은 아닙니다.
