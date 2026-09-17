# POST /give/paleggs/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/give/paleggs/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.PalEggs.Give`

## 용도

대상 플레이어에게 팰 알 하나 또는 여러 개를 지급합니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

알 지급 배열인 `PalEggs`를 포함하는 JSON 객체입니다. `EggID`는 [`ItemID`](https://paldeck.cc/items)입니다. 각 알에는 [`PalID`](https://paldeck.cc/pals)와 `PalTemplate` 중 하나만 지정해야 합니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/give-paleggs.md"

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
| `400` | `INVALID_REQUEST` | 본문에 `PalEggs` 배열이 없습니다. |
| `400` | `VALIDATION_FAILED` | 지급할 알 중 하나 이상이 잘못되었거나 가져올 수 없거나 인벤토리에 공간이 부족합니다. |

## 예제

### Steam 플레이어에게 레벨을 지정한 알 지급

```http
POST /v1/pdapi/give/paleggs/steam_76561198012345678
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

### PlayerUID로 템플릿 기반 알 지급

```http
POST /v1/pdapi/give/paleggs/6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09
```

```json
{
    "PalEggs": [
        { "EggID": "PalEgg_Dark_01", "PalTemplate": "dark_event_reward.json" }
    ]
}
```

## 활용 사례

- 팰을 즉시 생성하지 않고 이벤트 알을 지급합니다.
- 일반적인 알에는 `PalID`를, 내용물을 직접 설정한 알에는 `PalTemplate`을 사용하세요.
- 알의 [`ItemID`](https://paldeck.cc/items)가 잘못되었거나 플레이어 인벤토리에 공간이 없으면 요청이 실패할 수 있습니다.
