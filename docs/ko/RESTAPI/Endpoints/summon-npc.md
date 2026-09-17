# POST /summon/npc

**엔드포인트:** `POST /v1/pdapi/summon/npc`  
**인증:** Bearer 토큰  
**필요 권한:** `REST.Summon.NPC`

## 용도

지정된 맵 좌표에 NPC를 생성합니다.

## 요청 본문

| 필드 | 자료형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `NPCID` | 문자열 | 예 | NPC ID 또는 NPC Character ID입니다. |
| `X`, `Y`, `Z` | 숫자 | 예 | 맵 좌표입니다. |
| `Level` | 정수 | 아니요 | NPC 레벨입니다. 기본값은 `1`입니다. |
| `Uncapturable` | 불리언 | 아니요 | 포획을 막습니다. 기본값은 `false`입니다. |
| `DisableAI` | 불리언 | 아니요 | 일반 AI를 끕니다. 기본값은 `false`입니다. |

## 응답 스키마

--8<-- "_snippets/ko/restapi/schemas/summon-npc.md"

## 오류

일반적인 인증/요청 오류 외에 `VALIDATION_FAILED` 또는 `SUMMON_NPC_FAILED`를 반환할 수 있습니다.

## 예제

```http
POST /v1/pdapi/summon/npc
Authorization: Bearer <token>
Content-Type: application/json
```

```json
{
    "NPCID": "PIDF_Soldier_AssaultRifle",
    "Level": 30,
    "X": 230,
    "Y": -486,
    "Z": 4097
}
```
