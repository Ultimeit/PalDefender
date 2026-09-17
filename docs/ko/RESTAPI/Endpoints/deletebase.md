# POST /deletebase/{base_camp_id}



**엔드포인트:** `POST /v1/pdapi/deletebase/<base_camp_id>`

**인증:** Bearer 토큰

**필요 권한:** `REST.Base.Delete`

## 용도

거점 ID로 거점을 삭제합니다. 데이터를 삭제하는 관리자 작업입니다.

## 경로 매개변수

- `base_camp_id`: 거점 식별자입니다. 보통 길드/거점 데이터에서 복사합니다.

## 쿼리 매개변수

없습니다.

## 요청 본문

선택적으로 빈 JSON 객체를 보낼 수 있습니다. 요청을 전송하기 전에 ID를 확인하세요.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/deletebase.md"

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
| `400` | `INVALID_BASE_CAMP_ID` | 경로의 `base_camp_id`가 유효한 GUID가 아닙니다. |
| `500` | `BASE_CAMP_MANAGER_UNAVAILABLE` | 서버에서 `UPalBaseCampManager`에 접근할 수 없습니다. |
| `404` | `BASE_CAMP_NOT_FOUND` | 지정한 GUID와 일치하는 거점이 없습니다. |
| `500` | `DELETE_BASE_FAILED` | 거점을 찾았지만 파괴/정리에 실패했습니다. |

## 예제

### GUID로 거점 삭제

```http
POST /v1/pdapi/deletebase/13b9e8d7-4f2c-42a1-b79e-fc2a9186e4d5
```

### 다른 GUID의 거점 삭제

```http
POST /v1/pdapi/deletebase/81c2f0a4-6d7e-49fb-a11d-0d2f9f94b13c
```

## 활용 사례

- 운영진 검토 후 방치되거나 손상된 거점을 제거합니다.
- 삭제 전에 [GET /guilds](guilds.md)와 [GET /guild](guild.md)로 대상 거점을 정확히 확인하세요.
- 운영 절차에서 소유권과 백업을 확인하고 있지 않다면 이 엔드포인트를 정기 정리에 사용하지 마세요.
