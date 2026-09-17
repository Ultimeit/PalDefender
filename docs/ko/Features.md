# 기능 및 현재 상태

이 페이지는 PalDefender 1.9.1에서 사용자가 설정할 수 있는 기능을 정리합니다. 정확한 기본값은 [`Config.json`](./FileTypes/Config.md)을 참고하세요.

## 보호 기능

- 피해량, 스태미나, 탄약 및 거점 복제 감지는 각각 켜거나 끌 수 있습니다.
- Anti-Vacuum은 일반 아이템, 팰 알, 유물, 수기를 비정상적으로 먼 거리에서 획득하려는 시도를 차단합니다. `allowAdminCheats`를 켜면 관리자는 이 기능이 지원하는 검사를 우회할 수 있습니다.
- 잘못된 아이템, 팰 능력치, 작업대 제작법, 닥터 서지, 긴급 재생성 및 기타 서버 행동에 대한 검사는 공통 검증 계층에서 계속 수행됩니다.
- `BannedCampWorker`는 지정된 Character ID의 캐릭터를 거점에 배치하지 못하게 합니다.

`antiDupe...` 키로 제어하던 기존 기능은 현재 릴리스 빌드에 포함되지 않습니다. 새로운 거점 복제 감지 기능은 별개이며, `baseCampDupeDetectionEnabled`로 제어합니다.

## 관리 및 이벤트

- `/admingun` (`/agun`)은 현재 관리자 권한이 활성화된 플레이어에게 보호 기능이 적용된 게임 내 [관리자 총](./Commands/index.md)을 지급합니다.
- `/setting`으로 지원되는 Palworld 설정의 현재 값을 확인하거나 일시적으로 변경할 수 있습니다.
- `/findbases`는 비어 있거나 비활성 상태인 거점을 차례로 방문하여 확인하는 기능을 제공합니다.
- PalSummon은 전투 이벤트 이름, AI 및 피해량 집계 제어, 능력치 배율, 조건부 포획, 순위 결과, 보상 설정을 지원합니다. [`PalSummon.json`](./FileTypes/PalSummon.md)을 참고하세요.
- Discord 전송 대상은 `PalWebhooks`에서 설정합니다. 채팅, 명령어, 사망, 접속 및 퇴장, 소환, 오일 리그 이벤트, 부정행위 감지 알림을 전송할 수 있습니다.

## 하트비트

릴리스 빌드는 게임 준비가 완료된 후 10초마다 `https://pallink.net/api/heartbeat`로 하트비트를 전송합니다. 전송 데이터에는 월드/서버 GUID, 운영체제 로캘의 국가 코드, PalDefender 및 Palworld 버전, 실행 플랫폼(Windows/Wine/Proton), 프로세스 가동 시간, 현재 접속자 수·최대 접속자 수·누적 고유 플레이어 수가 포함됩니다. 플레이어 이름, 계정 ID, IP 주소, 채팅 메시지 또는 저장 데이터 내용은 포함되지 않습니다. 디버그 빌드에서는 전송하지 않습니다.

## REST API

인증이 필요한 REST API로 플레이어, 팰, 인벤토리, 기술, 성장 진행도, 길드, 차단, 메시지, 보상 및 서버 운영 작업을 처리할 수 있습니다. 1.9.0 버전에서는 [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md)과 [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md)도 추가되었습니다.
