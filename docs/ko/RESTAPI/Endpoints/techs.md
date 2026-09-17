# GET /techs/{player_identifier}



**엔드포인트:** `GET /v1/pdapi/techs/<player_identifier>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Techs.Read`

## 용도

플레이어의 기술 정보를 조회합니다. 기술 식별자는 [paldeck.cc/technology](https://paldeck.cc/technology)에서 검색할 수 있습니다.

## 경로 매개변수

- `player_identifier`: 대상 플레이어의 `UserId` 또는 `PlayerUID`입니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/techs.md"

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
| `400` | `REQUEST_FAILED` | 대상 플레이어, 플레이어 계정, 기술 데이터 또는 기술 테이블을 확인할 수 없습니다. |
| `500` | `REQUEST_TIMEOUT` | 내부 게임 스레드 콜백이 5초 안에 완료되지 않았습니다. |

## 예제

### UserID로 해금한 기술 조회

```http
GET /v1/pdapi/techs/gdk_2533274812345678
```

### PlayerUID로 해금한 기술 조회

```http
GET /v1/pdapi/techs/f0a1c3e9-7d5b-4a28-8c33-411fdc2e6b74
```

## 활용 사례

- 기술을 습득시키거나 제거하기 전에 플레이어가 해당 [`TechID`](https://paldeck.cc/technology)를 이미 가지고 있는지 확인합니다.
- 해금한 기술과 습득 가능한 기술을 구분하는 관리자 페이지를 만듭니다.
- 지원 작업 후 성장 정보를 확인합니다.
