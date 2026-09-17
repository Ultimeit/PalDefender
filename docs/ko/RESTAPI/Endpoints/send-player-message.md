# POST /SendPlayerMessage



**엔드포인트:** `POST /v1/pdapi/SendPlayerMessage`

**인증:** Bearer 토큰

**필요 권한:** `REST.Messages.Send.PlayerChat`<br>`REST.Messages.Send.GlobalChat`<br>`REST.Messages.Send.GuildChat`<br>`REST.Messages.Send.Log.Normal`<br>`REST.Messages.Send.Log.Important`<br>`REST.Messages.Send.Log.VeryImportant`

## 용도

대상 플레이어 한 명 또는 여러 명에게 메시지를 전송합니다.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

`SendType`, `Message` 및 `UserID` 또는 `UserIDs` 중 하나를 포함하는 JSON 객체입니다. 일반적인 `SendType` 값은 `PlayerChat`, `PlayerGlobalChat`, `PlayerGuildChat`, `PlayerLogNormal`, `PlayerLogImportant`, `PlayerLogVeryImportant`입니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/send-player-message.md"

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
| `400` | `EMPTY_BODY` | 요청 본문이 비어 있습니다. |
| `400` | `INVALID_JSON` | 요청 본문이 올바른 JSON이 아닙니다. |
| `400` | `VALIDATION_FAILED` | `SendType`, `Message`, `UserID` 또는 `UserIDs`가 없거나 비어 있거나 중복되었거나 자료형이 잘못되었습니다. |
| `400` | `PLAYER_NOT_FOUND` | 대상 사용자 ID 또는 플레이어 UID 중 하나 이상을 찾을 수 없습니다. |
| `400` | `SEND_MESSAGE_FAILED` | 검증은 통과했지만 서버가 메시지 전송 작업을 거부했습니다. |
| `400` | `REQUEST_FAILED` | 게임 스레드 콜백에서 예외가 발생했습니다. |
| `500` | `REQUEST_TIMEOUT` | 내부 게임 스레드 콜백이 5초 안에 완료되지 않았습니다. |

## 예제

### 사용자 한 명에게 플레이어 채팅 전송

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerChat",
    "UserID": "steam_76561198012345678",
    "Message": "상점에서 주문한 상품이 도착했습니다."
}
```

### 여러 형식의 대상 ID에 중요 로그 전송

```http
POST /v1/pdapi/SendPlayerMessage
```

```json
{
    "SendType": "PlayerLogImportant",
    "UserIDs": [
        "ps5_0f4b8c2d91aa34ef",
        "6d2e8b40-73ef-4f11-9bb8-2e91a36e2f09",
        "gdk_2533274812345678"
    ],
    "Message": "10분 후 이벤트가 시작됩니다."
}
```

## 활용 사례

- 선택한 플레이어에게 재시작 예고를 직접 전송합니다.
- 관리자 패널에서 지원 답변을 전송합니다.
- 대상이 한 명이면 `UserID`, 여러 명이면 `UserIDs`를 사용하세요. 둘을 동시에 지정하지 마세요.
