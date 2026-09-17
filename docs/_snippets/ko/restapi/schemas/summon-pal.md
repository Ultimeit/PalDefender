### 200 응답 스키마

| 필드 | 자료형 | 설명 |
| --- | --- | --- |
| `Summoned` | 객체 | 생성된 팰의 상세 정보입니다. |

`Summoned`에는 `Type`(`"Pal"`), `PalID`, `Level`, `Uncapturable`, `DisableAI`, `DamageMeter` 및 요청한 `X`, `Y`, `Z`가 포함됩니다. 템플릿을 사용했다면 `PalTemplate`도 반환됩니다.
