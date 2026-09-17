# POST /ReloadConfig



**엔드포인트:** `POST /v1/pdapi/ReloadConfig`

**인증:** Bearer 토큰

**필요 권한:** `REST.Reload.Config`

## 용도

서버 전체를 재시작하지 않고 PalDefender 설정을 다시 불러옵니다.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

선택적으로 빈 JSON 객체를 보낼 수 있습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/reload-config.md"

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

## 예제

### 설정 다시 불러오기

```http
POST /v1/pdapi/ReloadConfig
```

### 토큰 변경 후 다시 불러오기

```http
POST /v1/pdapi/ReloadConfig
```

## 활용 사례

- 지원되는 설정 파일의 변경 사항을 적용합니다.
- `Banlist.json`, 가져오기 규칙 또는 실행 중에 읽을 수 있는 다른 PalDefender 파일을 수정한 뒤 다시 불러옵니다.
- 다시 불러온 뒤에도 변경 사항이 적용되지 않으면 점검 시간에 서버를 재시작하세요.
