# GET /banlist



**엔드포인트:** `GET /v1/pdapi/banlist`

**인증:** Bearer 토큰

**필요 권한:** `REST.Banlist.Read`

## 용도

차단 목록에서 기록을 조회합니다. 차단 데이터는 `Config.json`이 아니라 `Banlist.json`에 저장됩니다.

## 경로 매개변수

없습니다.

## 쿼리 매개변수

- `active`: `true`, `false` 또는 `1`로 활성 여부를 필터링합니다.
- `entryType`: 차단 항목 유형으로 필터링합니다.
- `userId`: 사용자 ID로 필터링합니다.
- `ip` 또는 `userIP`: IP 주소로 필터링합니다.
- `issuerType`, `issuerName`, `issuerIP`: 제재를 적용한 주체의 메타데이터로 필터링합니다.
- `reason`: 사유 텍스트로 필터링합니다.
- `q`: 일반 텍스트 검색입니다.

## 요청 본문

요청 본문은 없습니다.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/banlist.md"

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

### 모든 차단 기록 조회

```http
GET /v1/pdapi/banlist
```

### Steam 사용자의 활성 차단 기록 검색

```http
GET /v1/pdapi/banlist?active=true&userId=steam_76561198012345678
```

### IP로 기록 검색

```http
GET /v1/pdapi/banlist?ip=203.0.113.42
```

## 활용 사례

- 플레이어나 IP가 현재 차단되어 있는지 확인합니다.
- 차단을 해제하기 전에 사유 또는 제재 주체로 검색합니다.
- API를 통해 `Banlist.json`을 조회하는 제재 관리 대시보드를 만듭니다.

## 관련 문서

- [POST /ban](ban.md), [POST /unban](unban.md), [POST /banip](banip.md), [POST /unbanip](unbanip.md).
