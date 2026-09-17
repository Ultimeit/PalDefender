### 200 응답 스키마

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `Meta` | 객체 | 대상 플레이어 메타데이터입니다. |
| `Progression` | 객체 | 성장, 재화, 처치, 포획 및 활동 데이터입니다. |

`Meta` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `PlayerUID` | 문자열 | Palworld 저장 데이터에서 사용하는 플레이어 UID입니다. |
| `Player` | 문자열 | 요청 경로에 지정한 플레이어 식별자입니다. |

`Progression` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `Player` | 객체 | 플레이어 레벨, 경험치, 미사용 능력치 포인트입니다. |
| `Currencies` | 객체 | 유물 및 기술 포인트 총량입니다. |
| `Bosses` | 객체 | 보스 처치 횟수 및 플래그입니다. |
| `Captures` | 객체 | 팰 포획 및 도축 횟수입니다. |
| `Activities` | 객체 | 제작, 던전, 낚시, 보물 및 기타 활동 횟수입니다. |

`Progression.Player` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `level` | 정수 | 현재 플레이어 레벨입니다. |
| `exp` | 정수 | 현재 경험치입니다. |
| `unusedStatusPoints` | 정수 | 플레이어의 미사용 능력치 포인트입니다. |

`Progression.Currencies` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `relics` | 객체 | 유물 유형을 키로 하는 유물 포인트 총량입니다. |
| `technologyPoints` | 정수 | 기술 포인트 총량입니다. |
| `ancientTechnologyPoints` | 정수 | 고대 기술 포인트 총량입니다. |

`Progression.Bosses` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `towerBossDefeatCounts` | 객체 | 보스 ID를 키로 하는 탑 보스 처치 횟수입니다. |
| `normalBossDefeatFlags` | 객체 | 보스 ID를 키로 하는 일반 보스 처치 플래그입니다. |
| `raidBossDefeatCounts` | 객체 | 보스 ID를 키로 하는 레이드 보스 처치 횟수입니다. |
| `totalBossDefeatCount` | 정수 | 탑 보스 처치 횟수 합계입니다. |
| `predatorDefeatCount` | 정수 | 포식자 처치 횟수입니다. |

`Progression.Captures` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `tribeCaptureCount` | 정수 | 전체 종족 포획 횟수입니다. |
| `palCaptureCounts` | 객체 | 팰 ID를 키로 하는 팰 포획 횟수입니다. |
| `palCaptureBonusCounts` | 객체 | 팰 ID를 키로 하는 팰 포획 보너스 횟수입니다. |
| `palButcherCounts` | 객체 | 팰 ID를 키로 하는 팰 도축 횟수입니다. |

`Progression.Activities` 객체 스키마:

| 필드 | 자료형 | 설명 |
|-------|------|-------------|
| `craftItemCounts` | 객체 | 아이템 ID를 키로 하는 제작 수량입니다. |
| `normalDungeonClearCount` | 정수 | 일반 던전 완료 횟수입니다. |
| `fixedDungeonClearCount` | 정수 | 고정 던전 완료 횟수입니다. |
| `oilrigClearCount` | 정수 | 오일 리그 완료 횟수입니다. |
| `palRankUpCounts` | 객체 | 팰 ID를 키로 하는 등급 상승 횟수입니다. |
| `arenaSoloClearCounts` | 객체 | 아레나 ID를 키로 하는 솔로 아레나 완료 횟수입니다. |
| `npcTalkCounts` | 객체 | NPC ID를 키로 하는 대화 횟수입니다. |
| `fishingCounts` | 객체 | 물고기 ID를 키로 하는 낚시 횟수입니다. |
| `foundTreasureCount` | 정수 | 발견한 보물 수입니다. |
| `campConqueredCount` | 정수 | 점령한 야영지 수입니다. |
| `firstFishingComplete` | 불리언 | 첫 낚시 완료가 기록되어 있는지 나타냅니다. |
