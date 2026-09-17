# POST /give/paltemplate/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/give/paltemplate/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.PalTemplates.Give`

## 용도

`Pals/Templates/`의 파일에서 팰 하나 또는 여러 마리를 가져와 지급합니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

템플릿 파일 이름 배열인 `PalTemplates`를 포함하는 JSON 객체입니다. 명확하게 표시하려면 `.json` 확장자를 포함할 수 있습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/give-paltemplate.md"

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
| `400` | `INVALID_REQUEST` | 본문에 `PalTemplates` 배열이 없습니다. |
| `400` | `VALIDATION_FAILED` | 템플릿 파일 이름 중 하나 이상이 잘못되었거나 가져올 수 없거나 팰 보관 공간이 부족합니다. |

## 예제

### Steam 플레이어에게 템플릿 팰 한 마리 지급

```http
POST /v1/pdapi/give/paltemplate/steam_76561198087654321
```

```json
{
    "PalTemplates": [
        "starter_pengullet.json"
    ]
}
```

### PS5 플레이어에게 레이드 보상 템플릿 지급

```http
POST /v1/pdapi/give/paltemplate/ps5_c481a77e22004b9d
```

```json
{
    "PalTemplates": [
        "raid_reward_01.json",
        "raid_reward_02.json"
    ]
}
```

## 활용 사례

- 보상에 특정 기술, 패시브, 개체값, 영혼 강화 수치, 별명 또는 작업 적성이 필요할 때 사용합니다.
- 먼저 [파일 유형/PalTemplate](../../FileTypes/PalTemplate.md)을 참고하여 템플릿을 만드세요.
- `Pals/ImportRules/`의 가져오기 규칙이 지급 전에 템플릿을 차단하거나 조정할 수 있습니다.
