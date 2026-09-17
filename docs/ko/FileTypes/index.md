# 📁 파일 유형

**PalDefender**는 서버 동작을 설정하고 기능을 확장할 수 있는 다양한 사용자 정의 파일을 지원합니다.
현재 지원되는 파일:
* `Config.json`
* `WhiteList.json`
* `Banlist.json`
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json`
* `RESTAPI/RESTConfig.json`
* `RESTAPI/Tokens/*.json`

---

## ⚡ 빠른 개요

### 🛠️ [Config.json](./Config.md)

서버 동작, 제재, 로그 기록 및 관리자 설정을 제어합니다.

* **보안:** 부정행위 방지(경고, 강제 퇴장, 계정 차단, IP 차단), 이름/단어 필터, SteamID 보호, 비정상 능력치/아이템 검사.
* **로그:** 채팅, RCON, 로그인, 사망, 소환, 건설 활동, 오일 리그 이벤트 기록.
* **관리자:** IP 허용 목록, 자동 로그인, 무적 모드/치트, 관리자 행동 공개 여부.
* **공지:** 접속 안내(MOTD), 플레이어 사망, 소환, 제재, 전리품 이벤트.
* **채팅 및 게임플레이 제한:** 메시지 길이, 재사용 대기시간 우회, PvP/PvE 피해량 상한, 벌목 제한.
* **기타:** RCON Base64 지원, 시작 실패 처리, 선택적으로 사용하는 중국어 명령어 모드.

---

### 👥 `WhiteList.json`

서버에 접속할 수 있는 대상을 지정합니다.
**사용자 ID**와 **IP 주소**를 모두 지원하며, 와일드카드로 지정한 IP 범위도 사용할 수 있습니다.

---

### 🚫 `Banlist.json`

계정 차단, 차단 해제, IP 차단 및 REST 제재 도구에서 사용하는 PalDefender 차단 기록을 저장합니다.

* 파일을 직접 수정하기보다는 `/ban`, `/unban`, `/banip`, `/unbanip` 또는 REST API를 사용하세요.
* 직접 수정해야 한다면 먼저 서버를 중지하거나, 수정 후 설정을 다시 불러오세요.

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

명령어로 사용자 정의 팰을 생성하거나 지급할 때 사용합니다.

* 팰의 **ID, 별명, 성별, 능력치(HP/SP/MP), 포만도, SAN, 희귀 여부, 기술, 개체값(IV), 패시브** 등을 지정합니다.
* 팰의 **전투 능력, 보조 능력, 작업 특성**을 자유롭게 설정할 수 있습니다.

---

### 📍 [PalSummon.json](./PalSummon.md)

지정된 위치에 사용자 정의 팰을 생성합니다.

* `PalTemplate`을 참조하고 **월드 좌표(X, Y, Z)**를 지정합니다.
* **포획 불가** 등의 옵션을 설정하고 특정 **상태 이상**(독, 익사, 화상 등)을 비활성화합니다.

---

### 🧾 [Pals/ImportRules/*.json](./PalImportRules.md)

사용자 정의 팰 템플릿을 가져올 때 적용되는 규칙을 제어합니다.

* `Pals/ImportRules/Default.json`에서 전체 제한을 설정합니다.
* `Pals/ImportRules/Anubis.json` 등의 파일로 팰별 예외 설정을 추가합니다.
* 제한을 넘는 값이 있으면 가져오기를 차단할지, 값을 상한에 맞출지 선택합니다.
* 금지된 패시브가 있으면 가져오기를 차단할지, 해당 패시브를 제거할지 선택합니다.

---

### 🌐 REST API 설정 파일

REST API 설정은 `RESTAPI/RESTConfig.json`에, Bearer 토큰은 `RESTAPI/Tokens/*.json`에 저장됩니다.

* `RESTConfig.json`은 API 활성화 여부, 바인딩 주소, 포트, 콘솔 로그 및 CORS 설정을 제어합니다.
* 각 토큰 파일에는 비밀 토큰과 권한이 들어 있어야 합니다. 토큰 값을 공개하지 마세요.
