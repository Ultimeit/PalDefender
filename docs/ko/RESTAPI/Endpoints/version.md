# GET /version



**엔드포인트:** `GET /v1/pdapi/version`

**인증:** Bearer 토큰

**필요 권한:** `REST.Version.Read`

## 용도

도구, 대시보드, 스크립트에서 API 작동 여부와 버전을 확인할 때 사용하세요.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/version.md"

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

### 작동 여부 및 버전 확인

```http
GET /v1/pdapi/version
```

## 활용 사례

- REST API 토큰 설정 후 인증이 정상적으로 작동하는지 확인합니다.
- 도구가 특정 PalDefender 버전 이상을 요구한다면 다른 엔드포인트 호출 전에 확인합니다.
- 가장 작은 읽기 전용 요청이므로 모니터링에 사용합니다.
