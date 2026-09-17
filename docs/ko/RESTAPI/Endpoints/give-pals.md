# POST /give/pals/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/give/pals/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Pals.Give`

## 용도

ID와 레벨로 팰 하나 또는 여러 마리를 지급합니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

팰 지급 배열인 `Pals`를 포함하는 JSON 객체입니다. 각 항목에 [`PalID`](https://paldeck.cc/pals)와 양수 `Level`이 필요합니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/give-pals.md"

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
| `400` | `INVALID_REQUEST` | 본문에 `Pals` 배열이 없습니다. |
| `400` | `VALIDATION_FAILED` | 지급할 팰 중 하나 이상이 잘못되었거나 플레이어의 팰 보관 공간이 부족합니다. |

## 예제

### GDK 플레이어에게 시작용 팰 지급

```http
POST /v1/pdapi/give/pals/gdk_2533274812345678
```

```json
{
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ]
}
```

### PlayerUID로 이벤트 팰 지급

```http
POST /v1/pdapi/give/pals/b7f4e91a-2c53-4d8f-a6e1-93c4bb62a7d1
```

```json
{
    "Pals": [
        { "PalID": "Anubis", "Level": 35 },
        { "PalID": "Kitsun", "Level": 25 }
    ]
}
```

## 활용 사례

- 템플릿 파일을 관리하지 않고 간단한 팰 보상을 지급합니다.
- `PalID`와 `Level`만 바꾸는 무작위 보상 스크립트에 사용합니다.
- 플레이어를 찾을 수 없거나 [`PalID`](https://paldeck.cc/pals)가 잘못되었거나 팰 보관 공간이 부족하면 요청이 실패할 수 있습니다.
