# POST /summon/pal

**엔드포인트:** `POST /v1/pdapi/summon/pal`  
**인증:** Bearer 토큰  
**필요 권한:** `REST.Summon.Pal`

## 용도

지정된 맵 좌표에 팰을 생성합니다. 요청에는 `PalID`와 `PalTemplate` 중 정확히 하나만 지정해야 합니다.

## 요청 본문

| 필드 | 자료형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `PalID` | 문자열 | 둘 중 하나 | 팰 종 ID입니다. `PalTemplate`과 함께 지정할 수 없습니다. |
| `PalTemplate` | 문자열 | 둘 중 하나 | `Pals/Templates/`의 파일 이름입니다. 템플릿의 팰과 레벨을 사용합니다. |
| `X`, `Y`, `Z` | 숫자 | 예 | 맵 좌표입니다. |
| `Level` | 정수 | 아니요 | `PalID`로 소환할 때의 레벨입니다. 기본값은 `1`이며 템플릿 사용 시 무시합니다. |
| `Uncapturable` | 불리언 | 아니요 | 포획을 막습니다. 기본값은 `false`입니다. |
| `DisableAI` | 불리언 | 아니요 | 일반 AI를 끕니다. 기본값은 `false`입니다. |
| `DisableDamageMeter` | 불리언 | 아니요 | 피해량 집계를 끕니다. 기본값은 `false`입니다. |
| `DisableStatuses` | 배열 | 아니요 | 적용을 막을 상태 이름입니다. |

!!! warning "최대 체력 설정 변경"
    `PalTemplate`을 사용하면 템플릿의 `HP`가 생성된 팰의 최대 체력이 됩니다. `HealthMultiplier`와 `HPMultiplier`는 더 이상 요청에서 허용하거나 응답에 반환하지 않으므로 기존 REST 연동에서 제거하세요.

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/summon-pal.md"

## 오류

일반적인 `INVALID_TOKEN`, `MISSING_PERMISSION`, `INVALID_JSON`, `REQUEST_FAILED`, `REQUEST_TIMEOUT` 응답 외에 `VALIDATION_FAILED`, `PAL_TEMPLATE_IMPORT_FAILED`, `SUMMON_PAL_FAILED`를 반환할 수 있습니다.

## 예제

```http
POST /v1/pdapi/summon/pal
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "PalTemplate": "ArenaBoss.json",
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "Uncapturable": true
}
```
