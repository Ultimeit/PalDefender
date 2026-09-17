# POST /learntech/{player_identifier}



**엔드포인트:** `POST /v1/pdapi/learntech/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Techs.Learn`

## 용도

플레이어에게 기술 하나, 여러 개 또는 전체를 습득시킵니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

`Technology`에는 단일 [`TechID`](https://paldeck.cc/technology), 문자열 `"All"` 또는 [`TechID`](https://paldeck.cc/technology) 문자열 배열을 지정할 수 있습니다. 배열 안에는 `"All"`을 넣지 마세요.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/learntech.md"

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
| `400` | `INVALID_REQUEST` | `Technology`가 없거나 요구되는 형식의 문자열/배열이 아닙니다. |
| `400` | `VALIDATION_FAILED` | `Technology` 배열에 문자열이 아닌 값, `All` 또는 잘못된 기술 식별자가 있습니다. |

## 예제

### Steam 플레이어에게 기술 하나 습득

```http
POST /v1/pdapi/learntech/steam_76561198087654321
```

```json
{
    "Technology": "Technology_ElecBaton"
}
```

### PS5 플레이어에게 여러 기술 습득

```http
POST /v1/pdapi/learntech/ps5_0f4b8c2d91aa34ef
```

```json
{
    "Technology": [
        "Technology_ElecBaton",
        "Technology_GrapplingGun"
    ]
}
```

### PlayerUID로 모든 기술 습득

```http
POST /v1/pdapi/learntech/92b8f6ac-1a3d-4a9e-8f52-cc741db8c20a
```

```json
{
    "Technology": "All"
}
```

## 활용 사례

- 지원 요청에 대응하여 누락된 제작법을 해금합니다.
- 테스트 계정의 모든 기술을 해금합니다.
- 요청을 보내기 전에 [paldeck.cc/technology](https://paldeck.cc/technology)에서 기술 ID를 확인하세요.
