# 🛠️ `Config.json`

`Config.json`은 처음 실행할 때 `<PalServer>/Pal/Binaries/Win64/PalDefender/`에 생성됩니다. 수정 전에 서버를 중지하거나, 변경 사항을 저장한 뒤 `/reloadcfg`를 실행하세요.

!!! note "자동으로 기록되는 설정"
    PalDefender는 현재 설정 항목을 이 파일에 다시 기록합니다. 아래에 없는 키는 폐기되었거나, 이전 설정을 변환할 때만 사용하거나, 현재 공개 빌드에서 사용할 수 없는 항목입니다.

## 일반 설정 및 제재

| 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `version` | 문자열 | 현재 버전 | PalDefender가 관리하는 설정 스키마/버전 표시입니다. |
| `MOTD` | 배열 | 메시지 3개 | 접속 안내 메시지입니다. 지원하는 치환 변수: `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}`, `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | 불리언 | `true` | PalDefender를 초기화할 수 없으면 서버를 종료합니다. 일부 호스팅 환경에서는 이를 충돌로 판단하여 재시작을 반복할 수 있습니다. |
| `preventAdminPasswordInChat` | 불리언 | `true` | 관리자 비밀번호가 채팅 메시지로 전송되지 않게 합니다. |
| `shouldWarnCheaters` | 불리언 | `true` | 자동 감지가 발생하면 플레이어에게 경고합니다. |
| `shouldWarnCheatersReason` | 불리언 | `false` | 경고에 감지 사유를 포함합니다. |
| `shouldKickCheaters` | 불리언 | `true` | 더 강한 제재가 활성화되어 적용되는 경우를 제외하고, 감지된 부정행위자를 강제 퇴장시킵니다. |
| `shouldBanCheaters` | 불리언 | `false` | 감지된 부정행위자의 계정을 차단합니다. |
| `shouldIPBanCheaters` | 불리언 | `false` | 감지된 부정행위자의 IP를 차단합니다. |
| `blockEmergencyRespawn` | 불리언 | `true` | 메뉴 → 긴급 재생성을 차단합니다. |

## RCON 및 로그

| 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `RCONTimeout` | 실수 | `31.0` | 비활성 RCON 연결의 시간 초과까지 걸리는 시간(초)입니다. |
| `RCONbase64` | 불리언 | `false` | Base64로 인코딩한 RCON 명령어를 허용합니다. |
| `logNetworking` | 불리언 | `false` | 지원되는 네트워크 로그를 기록합니다. 현재 공개 빌드에서는 네트워크 로그 기능이 비활성화되어 있습니다. |
| `logNetworkingToConsole` | 불리언 | `true` | 네트워크 로그 기능을 사용할 수 있을 때 콘솔에도 출력합니다. |
| `logChat` | 불리언 | `true` | 전체, 길드, 주변(Say) 채팅을 기록합니다. |
| `logRCON` | 불리언 | `false` | RCON 명령어를 기록합니다. |
| `logPlayerUID` | 불리언 | `false` | 관련 로그와 부정행위 감지 웹훅에 PlayerUID를 포함합니다. |
| `logPlayerIP` | 불리언 | `true` | 관련 로그와 부정행위 감지 웹훅에 IP 주소를 포함합니다. |
| `logPlayerDeaths` | 불리언 | `true` | 플레이어 사망 및 처치를 기록합니다. |
| `logPlayerLogins` | 불리언 | `true` | 플레이어 접속 및 퇴장을 기록합니다. |
| `logPlayerBuildings` | 불리언 | `true` | 지원되는 건설, 취소, 해체 및 팰 상자 이동 활동을 기록합니다. |
| `logPlayerSummons` | 불리언 | `true` | 플레이어의 레이드 보스 소환을 기록합니다. |
| `logPlayerCaptures` | 불리언 | `true` | 호환성을 위해 남겨 둔 설정입니다. 사용 가능한 이벤트를 신뢰할 수 없어 1.9.0에서는 포획 로그를 비활성화했습니다. |
| `logPlayerDamage` | 불리언 | `false` | 플레이어가 발생시킨 피해 이벤트와 보고된 원본/기본 피해량을 서버 콘솔에 기록합니다. 피해량 치트 감지와 독립적으로 작동합니다. |
| `BannedCampWorker` | 배열 | Panthalus 변종 | 거점에 배치할 수 없는 Character ID입니다. 대소문자를 구분하지 않으며, `BOSS_...` 같은 변종은 별도로 지정해야 합니다. |
| `logHelicopterKills` | 불리언 | `true` | 전투 헬리콥터 처치를 기록합니다. |
| `logCraftings` | 불리언 | `true` | 플레이어의 제작 활동을 기록합니다. |
| `logTechUnlocks` | 불리언 | `true` | 기술 해금을 기록합니다. |
| `logOpenOilrigBoxes` | 불리언 | `true` | 오일 리그 최종 보상 상자 이벤트를 기록합니다. |
| `OilrigGoalBoxLocktime` | 정수 | `300` | 오일 리그 최종 보상 상자의 잠금 유지 시간(초)입니다. |

## Discord 웹훅

`PalWebhooks`는 객체입니다. 특정 전송 대상을 끄려면 해당 URL을 비워 두세요. 웹훅은 전송 대기열을 사용하므로 요청이 몰려도 게임 스레드를 막지 않고 순차적으로 전송합니다.

| 하위 키 | 전송 내용 |
| --- | --- |
| `webhookURL_Chat` | 전체 및 주변(Say) 채팅 메시지. |
| `webhookURL_GuildChat` | 길드 이름이 포함된 길드 채팅 메시지. |
| `webhookURL_Commands` | 게임 내 채팅으로 실행한 명령어. 관리자와 명령어 전체 내용을 포함합니다. |
| `webhookURL_Deaths` | 사망 및 처치. `announcePlayerDeaths` 또는 `logPlayerDeaths`가 필요합니다. |
| `webhookURL_JoinLeave` | `announceConnections`를 켰을 때의 접속/퇴장 이벤트. `dontAnnounceAdminConnections`를 따릅니다. |
| `webhookURL_Summons` | 플레이어/관리자 소환 공지 및 피해량 집계가 활성화된 소환의 전체 결과. |
| `webhookURL_Oilrig` | 해당 `announce...` 설정을 켰을 때의 오일 리그 상자 및 헬리콥터 처치 이벤트. |
| `webhookURL_AntiCheats` | 자동 및 수동 검토용 부정행위 감지. UID/IP 포함 여부는 `logPlayerUID`와 `logPlayerIP`를 따릅니다. |

```json
"PalWebhooks": {
    "webhookURL_Chat": "",
    "webhookURL_GuildChat": "",
    "webhookURL_Commands": "",
    "webhookURL_Deaths": "",
    "webhookURL_JoinLeave": "",
    "webhookURL_Summons": "",
    "webhookURL_Oilrig": "",
    "webhookURL_AntiCheats": ""
}
```

## 관리자, 채팅 및 공지

| 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `useAdminWhitelist` | 불리언 | `true` | 관리자 로그인/명령어를 `adminIPs`의 IP로 제한합니다. |
| `adminAutoLogin` | 불리언 | `false` | 허용 목록의 IP로 접속하면 관리자 모드를 자동으로 켭니다. |
| `adminIPs` | 배열 | `127.0.0.1` | 서버 관리가 허용되는 정확한 IP 주소 및 지원되는 와일드카드 항목입니다. |
| `bannedChatWords` | 배열 | 일반적인 현금 거래 용어 | 대소문자를 구분하지 않는 채팅 필터 단어입니다. |
| `bannedNames` | 배열 | 알려진 악용 이름 | 로그인 시 거부할 플레이어 이름입니다. |
| `allowAdminCheats` | 불리언 | `false` | 관리자가 `adminCheats`의 명령어를 사용하고 일부 보호 기능을 우회할 수 있게 합니다. 관리자 총 자체는 게임 내 관리자 권한이 활성화되어 있기만 하면 됩니다. |
| `allowGodmodeOnehit` | 불리언 | `false` | 무적 모드 사용자가 한 방에 처치하는 피해를 줄 수 있게 합니다. |
| `adminCheats` | 배열 | 자동 생성 목록 | `allowAdminCheats`가 꺼져 있을 때 관리자 치트로 취급하는 명령어입니다. 이 목록은 RCON을 차단하지 않습니다. |
| `announceConnections` | 불리언 | `false` | 접속/퇴장을 채팅에 공지하고 관련 웹훅 이벤트를 활성화합니다. |
| `dontAnnounceAdminConnections` | 불리언 | `true` | 해당 공지에서 관리자의 접속/퇴장을 숨깁니다. |
| `announcePunishments` | 불리언 | `false` | 부정행위 감지로 자동 적용된 강제 퇴장/차단을 공지합니다. |
| `announcePlayerDeaths` | 불리언 | `false` | 플레이어 사망을 채팅에 공지합니다. |
| `announceOpenOilrigBoxes` | 불리언 | `false` | 오일 리그 상자 이벤트를 공지하고 관련 웹훅 이벤트를 활성화합니다. |
| `announceHelicopterKills` | 불리언 | `false` | 헬리콥터 처치를 공지하고 관련 웹훅 이벤트를 활성화합니다. |
| `announcePlayerSummons` | 불리언 | `false` | 플레이어의 레이드 보스 소환을 공지합니다. |
| `announceAdminSummons` | 불리언 | `false` | 관리자 소환 기능으로 생성한 팰을 공지합니다. |
| `announceAdminSummonsKill` | 불리언 | `true` | 관리자가 소환한 팰의 처치/사망을 공지합니다. |
| `chatBypassWait` | 불리언 | `true` | 채팅 메시지 사이의 기본 대기시간을 제거합니다. |
| `chatMessageMaxLen` | 정수 | `128` | 허용되는 채팅 메시지의 최대 길이입니다. |
| `useWhitelist` | 불리언 | `false` | `WhiteList.json`을 활성화합니다. |
| `whitelistMessage` | 문자열 | 자동 생성 문구 | 허용 목록에 없어 접속이 거부된 플레이어에게 표시할 메시지입니다. |
| `steamidProtection` | 불리언 | `true` | 동일한 UserId의 동시 중복 사용을 거부합니다. |

## 게임플레이 검증

| 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | 정수 | `100` | 건축물에 허용되는 최대 PvP 피해량입니다. |
| `pvpMaxToPalDamage` | 정수 | `1000` | 팰에 허용되는 최대 PvP 피해량입니다. |
| `pveMaxToPalBanThreshold` | 정수 | `900000` | 부정행위 감지에 사용하는 PvE 팰 피해량 임계값입니다. |
| `droppedPalPickupRange` | 정수 | `99999` | 떨어뜨린 팰을 주울 수 있는 최대 거리입니다. |
| `treeLimiter` | 실수 | `0.1` | 식생이 한꺼번에 파괴되는 것을 제한하기 위한 나무 파괴 이벤트 사이의 최소 간격(초)입니다. |
| `disableIllegalItemProtection` | 불리언 | `false` | 잘못된 아이템/모드 아이템 보호 기능을 끕니다. |
| `disableButchering` | 불리언 | `false` | 팰 도축을 차단합니다. |
| `disableRenaming` | 불리언 | `false` | 플레이어 이름 변경을 차단합니다. |
| `disablePalRenaming` | 불리언 | `false` | 팰 이름 변경을 차단합니다. |
| `doActionUponIllegalPalStats` | 불리언 | `true` | 불가능한 팰 능력치가 감지되면 설정된 부정행위 제재를 적용합니다. |
| `preventUnsupportedWorkbenchRecipes` | 불리언 | `true` | 해당 작업대에서 지원하지 않는 제작법을 차단합니다. |
| `preventDoctorSurgiExploit` | 불리언 | `true` | 닥터 서지 취약점 악용을 감지/차단합니다. |
| `doActionUponDoctorSurgiExploit` | 불리언 | `true` | 해당 취약점 악용에 설정된 부정행위 제재를 적용합니다. |
| `palStatsMaxRank` | 정수 | `-1` | 팰 강화 등급 상한입니다. `-1`이면 현재 게임의 제한을 자동으로 사용합니다. |
| `bannedTechnologies` | 배열 | 비어 있음 | 습득을 차단하고 발견 시 제거할 기술 ID입니다. |

## 부정행위 방지 기능 설정

| 키 | 자료형 | 기본값 | 설명 |
| --- | --- | --- | --- |
| `antiDupeEnabled` | 불리언 | `true` | 기존 AntiDupe 기능의 호환성 설정입니다. 현재 릴리스 빌드에서는 작동하지 않습니다. |
| `antiDupeBuildRateLimitSeconds` | 실수 | `1.5` | 기존 건설 사이 최소 간격입니다. 현재 작동하지 않습니다. |
| `antiDupeDismantleRateLimitSeconds` | 실수 | `1.5` | 기존 해체 사이 최소 간격입니다. 현재 작동하지 않습니다. |
| `antiDupeShowBlockMessage` | 불리언 | `true` | 기존 차단 메시지 표시 설정입니다. 현재 작동하지 않습니다. |
| `antiDupeBuildMessage` | 문자열 | 자동 생성 문구 | 기존 건설 차단 메시지입니다. 현재 작동하지 않습니다. |
| `antiDupeDismantleMessage` | 문자열 | 자동 생성 문구 | 기존 해체 차단 메시지입니다. 현재 작동하지 않습니다. |
| `antiVacuumEnabled` | 불리언 | `true` | 원거리 획득(흡입) 방지 기능을 켭니다. |
| `antiVacuumBlockAutoPickup` | 불리언 | `true` | 일반 자동 획득에 원거리 획득 방지 검사를 적용합니다. |
| `antiVacuumBlockRelicObtain` | 불리언 | `true` | 유물 획득에 검사를 적용합니다. |
| `antiVacuumBlockNoteObtain` | 불리언 | `true` | 수기 획득에 검사를 적용합니다. |
| `antiVacuumBlockEggPickup` | 불리언 | `true` | 알 획득에 검사를 적용합니다. |
| `antiVacuumMaxPickupDistance` | 실수 | `800.0` | 보호 대상 요청에 허용되는 최대 획득 거리입니다. |
| `antiVacuumShowBlockMessage` | 불리언 | `true` | 획득이 차단되면 플레이어에게 메시지를 표시합니다. |
| `antiVacuumBlockMessage` | 문자열 | 자동 생성 문구 | 원거리 획득이 차단되었을 때 표시할 메시지입니다. |
| `staminaCheatDetectionEnabled` | 불리언 | `true` | 의심스러운 스태미나 관련 행동 감지를 켭니다. |
| `baseCampDupeDetectionEnabled` | 불리언 | `true` | 거점 복제 감지를 켭니다. |
| `damageCheatDetectionEnabled` | 불리언 | `true` | 피해량 치트 감지를 켭니다. |
| `damageCheatDetectionTolerancePercent` | 실수 | `5.0` | 보고된 원본 피해량과 재계산한 `BasePower × AttackWithBuff` 사이에 허용되는 차이(%)입니다. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | 실수 | `1.5` | 장착한 무기의 고정 `AttackValue`에 대한 배율로 지정하는 무기 `BasePower` 상한입니다. |
| `ammoCheatDetectionEnabled` | 불리언 | `true` | 탄약/무기 상태 치트 감지를 켭니다. |

설정 호환성을 위해 `antiDupe...` 키는 계속 생성되지만, 기존 AntiDupe 기능은 현재 릴리스 빌드에서 비활성화되어 있습니다. 기능이 다시 활성화되기 전에는 이 설정에 의존하지 마세요.

## 이전 설정 변환용 키

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS`, `PalImport_MaxIV`는 이전 설치 환경의 설정을 [`Pals/ImportRules/Default.json`](./PalImportRules.md)으로 변환할 때만 읽습니다. 현재 `Config.json`에는 더 이상 기록하지 않습니다.

이전 키인 `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd`, `blockTowerBossCapture`는 현재 설정에 포함되지 않습니다. 차단 기록은 `Banlist.json`에서 관리합니다.
