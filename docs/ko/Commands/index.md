# 명령어

## 명령어란?

명령어는 게임에 특정 동작을 지시하는 텍스트입니다. 채팅에 입력하여 순간이동, 생물 생성, 플레이어 관리 등을 수행할 수 있습니다. 보통 <span class="var-command">/</span>로 시작하며 뒤에 명령어 이름과 필요한 인수를 입력합니다.

## 누가 사용할 수 있나요?

**현재 일반 플레이어가 사용할 수 있는 명령어는 없습니다.**
현재 버전에서는 관리자 및 RCON 명령어만 제공합니다.

## 명령어 목록

!!! note "명령어 문법"
    <span class="var-command">/명령어_이름&nbsp;</span><span class="var-command-arg">&lt;필수_인수&gt;&nbsp;</span><span class="var-command-optional">[선택_인수={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;필수_인수&gt;</span> → 반드시 입력해야 합니다.<br>
    <span class="var-command-optional">[선택_인수={?}]</span> → 생략할 수 있습니다. <span class="var-command-optional">{?}</span>는 생략했을 때 사용하는 기본값입니다.
    </p>
    <p>
    인수에는 여러 자료형이 있습니다. 주로 <span class="var-string">문자열</span>, <span class="var-number">숫자</span>, <span class="var-float">실수</span>, <span class="var-bool">불리언</span>을 사용합니다. 특정 디렉터리의 <span class="file">파일 이름</span>이나 <span class="var-filter">필터</span>처럼 복잡한 인수를 받기도 합니다.
    </p>

!!! tip "ID 조회"
    `PalID`는 [paldeck.cc/pals](https://paldeck.cc/pals), `ItemID`는 [paldeck.cc/items](https://paldeck.cc/items), `TechID`는 [paldeck.cc/technology](https://paldeck.cc/technology), `BuildingID`는 [paldeck.cc/buildings](https://paldeck.cc/buildings), `PassiveID`는 [paldeck.cc/passives](https://paldeck.cc/passives), 기술 ID는 [paldeck.cc/skills](https://paldeck.cc/skills)에서 확인하세요.

??? note "RCON 전용"
    ??? info "/getrconcmds"
        **문법:** `/getrconcmds`

        **설명:** RCON에서 사용할 수 있는 모든 명령어와 필수 인수 개수를 반환합니다.

        **인수:**

        - 없음

        **사용 조건:** `RCON`

        **예제:**
        ```
        /getrconcmds
        ```

??? note "서버 관리"
    ??? info "/version"
        **문법:** `/version`

        **설명:** Palworld 게임 버전과 PalDefender 버전을 표시합니다. RCON에서는 JSON을 반환합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /version
        ```

    ??? info "/reloadcfg"
        **문법:** `/reloadcfg`

        **설명:** `Config.json`, `WhiteList.json` 및 PalDefender 차단 데이터를 다시 불러옵니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **문법:** `/addadminip <IP>`

        **설명:** 관리자 허용 목록에 IP 주소를 추가합니다.

        **인수:**

        - `<IP>`: 관리자로 허용할 IP 주소입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **문법:** `/setadmin <UserId>`

        **설명:** 플레이어에게 관리자 권한을 일시적으로 부여하거나 해제합니다.

        **인수:**

        - `<UserId>`: 관리자 권한을 부여하거나 해제할 플레이어 ID입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **문법:** `/pgbroadcast <Message>`

        **설명:** 서버의 모든 플레이어에게 메시지를 보냅니다.

        **인수:**

        - `<Message>`: 전체 전송할 메시지입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /pgbroadcast "곧 서버를 재시작합니다."
        ```

    ??? info "/adminlogin"
        **문법:** `/adminlogin <password>`

        **설명:** 관리자 모드로 로그인합니다. 인수에 관리자 비밀번호를 입력해야 합니다.

        **인수:**

        - `<password>`: 관리자 비밀번호입니다.

        **사용 조건:** `Chat`

        **예제:**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **문법:** `/adminlogout`

        **설명:** 관리자 모드에서 로그아웃합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **문법:** `/iwantplayerlist`

        **설명:** 게임 내 플레이어 목록 오버레이를 켭니다. ESC를 누르면 각 플레이어의 UserId와 Player UID를 확인할 수 있습니다. 게임 화면에서 상세 플레이어 정보를 확인하려는 관리자와 플레이어에게 유용합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **문법:** `/getpos [UserId]`

        **설명:** 순간이동이나 소환 등에 사용할 현재 월드 위치를 조회합니다. [UserId]를 지정하면 해당 플레이어의 위치를 조회합니다.

        **인수:**

        - `[UserId]`: (선택) 위치를 조회할 플레이어 ID입니다. 생략하면 자신의 위치를 조회합니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **문법:** `/settime <hour>`

        **설명:** Palworld의 시간을 변경합니다. `0`부터 `23`까지의 시각 또는 `day`, `night`를 지정할 수 있습니다.

        **인수:**

        - `<hour>`: 시각 값입니다(0–23, day, night).

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/togglepvp"
        **문법:** `/togglepvp`

        **설명:** 현재 서버 실행 세션에서 PvP를 켜거나 끕니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /togglepvp
        ```

    ??? info "/alert"
        **문법:** `/alert <message>`

        **설명:** 서버의 모든 플레이어에게 알림을 전송합니다. 일반적으로 화면에서 눈에 잘 띄게 표시됩니다.

        **인수:**

        - `<message>`: 알림으로 전체 전송할 메시지입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /alert 5분 후 서버를 재시작합니다!
        ```

    ??? info "/send"
        **문법:** `/send <type> <UserId> <Message>`

        **설명:** 특정 플레이어에게 채팅 또는 로그 메시지를 보냅니다.

        **인수:**

        - `<type>`: 전송할 메시지 유형입니다. 사용 가능한 값:
             - `msg`: 일반 채팅 메시지.
             - `log`: 일반 로그 메시지(흰색, 짧게 표시, 큰 글꼴).
             - `ilog`: 중요 로그 메시지(파란색, 더 오래 표시).
             - `vilog`: 매우 중요한 로그 메시지(파란색, 아주 오래 표시).
        - `<UserId>`: 메시지를 받을 플레이어 ID입니다.
        - `<Message>`: 전송할 메시지 내용입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /send msg steam_76500000000000000 Qonzer 할인 행사를 놓치지 마세요!
        /send log steam_76500000000000000 Qonzer 할인 행사를 놓치지 마세요!
        /send ilog steam_76500000000000000 Qonzer 할인 행사를 놓치지 마세요!
        /send vilog steam_76500000000000000 Qonzer 할인 행사를 놓치지 마세요!
        ```

    ??? info "/resetoilrig"
        **문법:** `/resetoilrig <lv30|lv55|lv60|all>`

        **설명:** 선택한 오일 리그 또는 현재 관리 중인 모든 오일 리그를 초기화합니다.

        **사용 조건:** `Chat`, 게임 내 관리자 권한이 활성화되어 있어야 합니다.

        **예제:**
        ```
        /resetoilrig all
        ```

    ??? info "/setting"
        **문법:** `/setting list [filter]` 또는 `/setting <setting_name> <get|set|add|sub> [value]`

        **설명:** 지원되는 `UPalGameSetting`의 현재 값을 확인하거나 변경합니다. 이름은 대소문자를 구분하지 않으며 대상을 유일하게 식별하는 접두어나 부분 문자열도 허용합니다. 실험적인 기능으로 영구 월드 설정을 대체하지 않으며, 클라이언트에는 캐시된 값이 계속 표시될 수 있습니다.

        - `list [filter]`: 지원되는 정수, 실수, 불리언, 바이트 및 열거형 필드를 나열합니다.
        - `get`: 값을 읽습니다.
        - `set`: 지원되는 모든 자료형의 값을 설정합니다. 불리언에는 `true/false`, `on/off`, `yes/no`, `1/0`을, 열거형에는 숫자 또는 항목 이름을 사용할 수 있습니다.
        - `add` / `sub`: 숫자 값만 변경합니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /setting list death
        /setting PalDeathPenaltyTime get
        /setting PalDeathPenaltyTime set 10
        ```

    ??? info "/resetbosstower"
        **문법:** `/resetbosstower <BossType|all>`

        **설명:** 디버그 빌드 전용 명령어로 탑 보스 인스턴스 하나 또는 초기화 가능한 모든 탑 보스를 초기화합니다. 단일 대상에는 유효한 `EPalBossType` 이름을 사용해야 합니다. 공개 릴리스 빌드에서는 사용할 수 없습니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /resetbosstower all
        ```

    ??? info "/showbosses"
        **문법:** `/showbosses`

        **설명:** 현재 보스의 정적 정보를 `PalDefender/Logs/BossInfo.json`에 기록하는 디버그 빌드 전용 데이터 추출 명령어입니다. 공개 릴리스 빌드에서는 사용할 수 없습니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

??? note "거점 관리"
    ??? info "/findunusedbases (별칭: /findbases)"
        **문법:** `/findbases [empty|inactive|unused|all] [days=N] [builds<=N]`

        **대화형 문법:** `/findbases visit [filters]`, `/findbases next`, `/findbases kill [next]`

        **설명:** 비어 있거나 비활성 상태이거나 사용되지 않는 거점을 검색합니다. `visit`는 채팅 전용 검토 목록을 만들고 첫 번째 결과로 순간이동합니다. `next`는 다음 거점으로 이동하며, `kill`은 선택한 거점을 파괴합니다. `kill next`는 파괴 후 다음 거점으로 이동합니다. 파괴는 되돌릴 수 없으므로 각 대상을 먼저 확인하세요.

        - `empty`: 작업 팰이 없고 건축물 수가 기본 상한(또는 `builds<=N`) 이하인 거점입니다.
        - `inactive`: 접속 중인 길드 멤버가 없고 최소 `days`일(기본 `30`) 동안 비활성 상태인 거점입니다.
        - `unused`: 비어 있거나 비활성 상태인 거점입니다.
        - `all`: 직접 지정한 필터를 적용하여 모든 거점을 나열합니다.

        **사용 조건:** 목록 조회는 `Chat`과 `RCON`을 지원합니다. visit/next/kill은 게임 내 채팅과 관리자 권한이 필요합니다.

        **예제:**
        ```
        /findbases empty builds<=5
        /findbases inactive days=14
        /findbases visit unused days=30
        /findbases kill next
        ```

    ??? info "/getnearestbase"
        **문법:** `/getnearestbase [X] [Y] [Z]`

        **설명:** 캐릭터에서 가장 가까운 거점을 소유한 길드 이름을 알려 줍니다.

        **참고:** **RCON**에는 위치를 확인할 플레이어 캐릭터가 없으므로 모든 위치 매개변수(`[X]` `[Y]` `[Z]`)가 **필수**입니다.

        **인수:**

        - `[X]`: (선택) X 좌표입니다.
        - `[Y]`: (선택) Y 좌표입니다.
        - `[Z]`: (선택) Z 좌표입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **문법:** `/gotonearestbase [X] [Y] [Z]`

        **설명:** 해당 위치에서 가장 가까운 거점으로 순간이동합니다.

        **참고:** **RCON**에는 위치를 확인할 플레이어 캐릭터가 없으므로 모든 위치 매개변수(`[X]` `[Y]` `[Z]`)가 **필수**입니다.

        **인수:**

        - `[X]`: (선택) X 좌표입니다.
        - `[Y]`: (선택) Y 좌표입니다.
        - `[Z]`: (선택) Z 좌표입니다.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **문법:** `/killnearestbase [X] [Y] [Z]`

        **설명:** 가장 가까운 거점을 파괴합니다(**주의해서 사용하세요!**).

        **참고:** **RCON**에는 위치를 확인할 플레이어 캐릭터가 없으므로 모든 위치 매개변수(`[X]` `[Y]` `[Z]`)가 **필수**입니다.

        **인수:**

        - `[X]`: (선택) X 좌표입니다.
        - `[Y]`: (선택) Y 좌표입니다.
        - `[Z]`: (선택) Z 좌표입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "플레이어 관리"
    ??? info "/kick"
        **문법:** `/kick <UserId> [Reason="Kicked by Admin."]`

        **설명:** 플레이어를 서버에서 강제 퇴장시킵니다.

        **인수:**

        - `<UserId>`: 강제 퇴장시킬 플레이어 ID입니다.
        - `[Reason]`: (선택) 강제 퇴장 사유입니다. 기본값: "Kicked by Admin."(관리자에 의해 강제 퇴장됨).

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /kick steam_76500000000000000 "채팅 도배"
        ```

    ??? info "/ban"
        **문법:** `/ban <UserId> [Reason="Banned by Admin."]`

        **설명:** 플레이어를 차단하고 서버에서 강제 퇴장시킵니다.

        **인수:**

        - `<UserId>`: 차단할 플레이어 ID입니다.
        - `[Reason]`: (선택) 차단 사유입니다. 기본값: "Banned by Admin."(관리자에 의해 차단됨).

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /ban gdk_25300000000000000 "부정행위"
        ```

    ??? info "/ipban"
        **문법:** `/ipban <UserId> [Reason="Banned by Admin."]`

        **설명:** 플레이어의 IP 주소를 차단하고 서버에서 강제 퇴장시킵니다.

        **인수:**

        - `<UserId>`: IP를 차단할 플레이어 ID입니다.
        - `[Reason]`: (선택) 차단 사유입니다. 기본값: "Banned by Admin."(관리자에 의해 차단됨).

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **문법:** `/banip <IP>`

        **설명:** IP 주소의 서버 접속을 차단합니다.

        **인수:**

        - `<IP>`: 차단할 IP 주소입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **문법:** `/unbanip <IP>`

        **설명:** 차단 목록에서 IP 주소를 제거합니다.

        **인수:**

        - `<IP>`: 차단을 해제할 IP 주소입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/unban"
        **문법:** `/unban <UserId> [Reason="Unbanned by admin."]`

        **설명:** PalDefender 차단 목록에서 UserId를 제거합니다.

        **인수:**

        - `<UserId>`: 차단을 해제할 UserId입니다.
        - `[Reason]`: (선택) 차단 해제 작업에 기록할 사유입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /unban steam_76500000000000000 "이의 신청 승인"
        ```

    ??? info "/getip"
        **문법:** `/getip <UserId>`

        **설명:** 플레이어의 IP 주소를 표시합니다.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **문법:** `/whitelist_add <UserId>`

        **설명:** 허용 목록에 UserId를 추가합니다.

        **인수:**

        - `<UserId>`: 허용 목록에 추가할 플레이어 ID입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **문법:** `/whitelist_remove <UserId>`

        **설명:** 허용 목록에서 UserId를 제거합니다.

        **인수:**

        - `<UserId>`: 허용 목록에서 제거할 플레이어 ID입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **문법:** `/whitelist_get`

        **설명:** 허용 목록의 전체 플레이어를 표시합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **문법:** `/imcheater`

        **설명:** 서버가 부정행위에 어떻게 대응하는지 테스트할 때 사용합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **문법:** `/spectate`

        **설명:** 관전 모드를 켭니다. 단축키 `\`를 누르는 것과 같지만 콘솔 플레이어 등 단축키를 사용할 수 없는 경우에도 실행할 수 있습니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /spectate
        ```

??? note "플레이어 캐릭터"
    ??? info "/tp"
        **문법:**
        다음 형식을 사용할 수 있습니다:

        - `/tp <UserId>`
        - `/tp <UserId1> <UserId2>`
        - `/tp <X> <Y>`
        - `/tp <X> <Y> <Z>`
        - `/tp <UserId> <X> <Y>`
        - `/tp <UserId> <X> <Y> <Z>`
        - `/tp home`
        - `/tp oilrig`
        - `/tp oilrig:Lv30`
        - `/tp oilrig:Lv55`
        - `/tp oilrig:Lv60`

        **설명:** 자신 또는 지정한 플레이어를 다른 플레이어, 좌표, 가장 가까운 소유 거점 또는 오일 리그로 순간이동시킵니다.

        **참고:** RCON에는 게임 내 캐릭터가 없으므로 순간이동시킬 플레이어를 반드시 지정해야 합니다.

        **인수:**

        - `<UserId>`: 이동 목적지가 되는 플레이어입니다. 추가 인수를 지정하면 순간이동시킬 플레이어를 뜻합니다.
        - `<UserId1>`: 순간이동시킬 플레이어입니다.
        - `<UserId2>`: 이동 목적지가 되는 플레이어입니다.
        - `<X> <Y> [Z]`: 맵 좌표입니다. `Z`를 생략하면 PalDefender가 사용할 수 있는 지면 높이를 찾습니다.
        - `home`: 가장 가까운 소유 거점으로 순간이동합니다.
        - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60`: 오일 리그로 순간이동합니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        /tp 100 -250
        /tp oilrig:Lv60
        ```

    ??? info "/give_exp"
        **문법:** `/give_exp <UserId> <Amount>`

        **설명:** 플레이어에게 경험치를 지급합니다.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<Amount>`: 지급할 경험치입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **문법:** `/giveme_exp <Amount>`

        **설명:** 자신에게 경험치를 지급합니다.

        **인수:**

        - `<Amount>`: 지급할 경험치입니다.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **문법:** `/renameplayer <UserId> <NewName>`

        **설명:** 플레이어의 별명을 변경합니다.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<NewName>`: 새 별명입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /renameplayer steam_76500000000000000 새별명
        ```

    ??? info "/givestats"
        **문법:** `/givestats <UserId> [Count=1]`

        **설명:** 플레이어에게 미사용 능력치 포인트를 지급합니다. 음수이면 차감합니다. 이미 사용한 포인트에는 영향을 주지 않습니다.

        **인수:**

        - `<UserId>`: 능력치 포인트를 받을 플레이어 ID입니다.
        - `[Count]`: (선택) 지급할 미사용 능력치 포인트입니다. 음수이면 차감합니다. 기본값: 1.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **문법:** `/givemestats [Count=1]`

        **설명:** 자신에게 미사용 능력치 포인트를 지급합니다. 음수이면 차감합니다. 이미 사용한 포인트에는 영향을 주지 않습니다.

        **인수:**

        - `[Count]`: (선택) 자신에게 지급할 미사용 능력치 포인트입니다. 음수이면 차감합니다. 기본값: 1.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **문법:** `/godmode [on/off]`

        **설명:** 상태 이상 면역을 포함한 무적 상태를 부여하고 음식 소모를 막으며, 활성화 시 체력을 회복합니다. 설정에서 허용하면 모든 대상을 한 방에 처치할 수도 있습니다.

        **인수:**

        - `[on/off]`: (선택) 무적 모드를 명시적으로 켜거나 끕니다. 생략하면 현재 상태를 전환합니다.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

    ??? info "/admingun (별칭: /agun)"
        **문법:** `/admingun`

        **설명:** 게임 내 관리자 권한이 활성화된 플레이어에게 보호 기능이 적용된 관리자 총을 지급합니다. 캐릭터를 즉시 처치하고 맵 오브젝트를 파괴하며 식생에 최대 피해를 줍니다. 탄약과 내구도는 무제한이며 버리기, 판매, 외부 컨테이너로 이동할 수 없습니다. 보관 오브젝트를 파괴할 때 웅크리면 내용물도 삭제하고, 서 있으면 내용물을 보존합니다. 사망, 게임 로그아웃 또는 관리자 로그아웃 시 총이 제거되며 다시 요청하면 기존 총을 대체합니다.

        **사용 조건:** `Chat`, 게임 내 관리자 권한이 활성화되어 있어야 합니다. `allowAdminCheats`는 필요하지 않습니다.

        **예제:**
        ```
        /agun
        ```

??? note "길드 관리"
    ??? info "/setguildleader"
        **문법:** `/setguildleader <UserId>`

        **설명:** 대상 플레이어를 현재 소속 길드의 길드장으로 지정합니다.

        **인수:**

        - `<UserId>`: 길드장으로 지정할 플레이어 ID입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **문법:** `/exportguilds`

        **설명:** 서버의 모든 길드 정보를 Pal/Binaries/Win64/PalDefender/guildexport.json으로 내보냅니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /exportguilds
        ```
        출력 파일 예: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "아이템"
    ??? info "/give"
        **문법:** `/give <UserId> <ItemId> [Amount=1]`

        **설명:** 플레이어에게 아이템을 지급합니다. 수량을 지정할 수 있습니다.

        **인수:**

        - `<UserId>`: 아이템을 받을 플레이어 ID입니다.
        - `<ItemId>`: 지급할 아이템입니다.
        - `[Amount]`: (선택) 수량입니다. 기본값: 1.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **문법:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **설명:** 한 명령어로 플레이어에게 여러 아이템을 지급합니다. 콜론 뒤에 각 아이템의 수량을 지정할 수 있습니다.

        **인수:**

        - `<UserId>`: 아이템을 받을 플레이어 ID입니다.
        - `<ItemId>[:<Amount>] ...`: 아이템 및 선택적인 수량 목록입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **문법:** `/giveme <ItemId> [Amount=1]`

        **설명:** 자신에게 아이템을 지급합니다. 수량을 지정할 수 있습니다.

        **인수:**

        - `<ItemId>`: 자신에게 지급할 아이템입니다.
        - `[Amount]`: (선택) 수량입니다. 기본값: 1.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **문법:** `/delitem <UserId> <ItemId> [Amount=1]`

        **설명:** 플레이어의 아이템을 지정한 수량만큼 삭제합니다. 기본값 `1`은 해당 아이템 하나만 삭제합니다. 모두 삭제하려면 `1` 대신 `all`을 사용하세요.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<ItemId>`: 삭제할 아이템입니다.
        - `[Amount]`: (선택) 삭제할 수량입니다. 기본값: 1. 해당 아이템을 모두 삭제하려면 `all`을 사용하세요.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **문법:** `/give_relic <UserId> <RelicType> [Amount]`

        **설명:** 플레이어에게 선택한 유형의 유물 포인트를 지급합니다.

        **인수:**

        - `<UserId>`: 유물 포인트를 받을 플레이어 ID입니다.
        - `<RelicType>`: 지급할 유물 유형입니다.

        - `[Amount]`: 선택적으로 지정할 유물 포인트 지급량입니다. 기본값은 `1`입니다.

        **지원되는 유물 유형:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /give_relic steam_76500000000000000 CapturePower 5
        ```

    ??? info "/giveme_relic"
        **문법:** `/giveme_relic <RelicType> [Amount]`

        **설명:** 자신에게 선택한 유형의 유물 포인트를 지급합니다.

        **인수:**

        - `<RelicType>`: 지급할 유물 유형입니다.

        - `[Amount]`: 선택적으로 지정할 자신의 유물 포인트 지급량입니다. 기본값은 `1`입니다.

        **지원되는 유물 유형:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /giveme_relic CapturePower 5
        ```


    ??? info "/delitems"
        **문법:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **설명:** 한 명령어로 플레이어의 여러 아이템을 삭제합니다. 콜론 뒤에 각 아이템의 수량을 지정할 수 있습니다. 해당 아이템을 모두 삭제하려면 `1` 대신 `all`을 사용하세요.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<ItemId>[:<Amount>] ...`: 아이템 및 선택적인 수량 목록입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **문법:** `/clearinv <UserId> [Container=items] ...`

        **설명:** 플레이어 인벤토리에서 지정한 컨테이너를 비웁니다. 사용 가능한 컨테이너: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot`, `all`.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `[Container] ...`: (선택) 비울 컨테이너입니다. 기본값: items.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "팰"
    ??? info "/givepal"
        **문법:** `/givepal <UserId> <PalId> [Level=1]`

        **설명:** 플레이어에게 지정한 레벨의 팰을 지급합니다.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<PalId>`: 지급할 팰입니다.
            - **참고:** `WeaselDragon`(칠렛)처럼 팰 ID를 사용하세요. 전체 목록은 [paldeck.cc/pals](https://paldeck.cc/pals)에서 확인할 수 있습니다.
        - `[Level]`: (선택) 팰 레벨입니다. 기본값: 1.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **문법:** `/givepal_j <UserID> <PalTemplate>`

        **설명:** [PalTemplate](../FileTypes/PalTemplate.md) 파일에 정의된 팰을 플레이어에게 지급합니다. JSON을 직접 입력하는 방식은 더 이상 지원하지 않으며 파일 이름만 사용할 수 있습니다.

        **참고:** 파일 이름에 .json 확장자를 넣지 않아도 됩니다. 생략하면 자동으로 추가합니다.

        **인수:**

        - `<UserID>`: 플레이어 ID입니다.
        - `<PalTemplate>`: PalTemplate 파일 이름입니다([PalTemplate](../FileTypes/PalTemplate.md) 참고).

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **문법:** `/givemepal <PalId> [Level=1]`

        **설명:** 자신에게 지정한 레벨의 팰을 지급합니다.

        **인수:**

        - `<PalId>`: 자신에게 지급할 팰입니다.
            - **참고:** `WeaselDragon`(칠렛)처럼 팰 ID를 사용하세요. 전체 목록은 [paldeck.cc/pals](https://paldeck.cc/pals)에서 확인할 수 있습니다.
        - `[Level]`: (선택) 팰 레벨입니다. 기본값: 1.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **문법:** `/givemepal_j <PalTemplate>`

        **설명:** [PalTemplate](../FileTypes/PalTemplate.md) 파일에 정의된 팰을 자신에게 지급합니다. JSON을 직접 입력하는 방식은 더 이상 지원하지 않으며 파일 이름만 사용할 수 있습니다.

        **인수:**

        - `<PalTemplate>`: PalTemplate 파일 이름입니다([PalTemplate](../FileTypes/PalTemplate.md) 참고).

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **문법:**
        다음 형식을 사용할 수 있습니다:

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **설명:** 실행자 기준 위치 또는 지정한 절대 좌표에 팰을 생성합니다. **RCON에서는 x, y, z를 반드시 지정해야 합니다!**

        **참고:** 레벨을 제외한 모든 능력치는 무작위로 결정됩니다.

        **인수:**
        - `<PalID>`: 생성할 팰입니다.
        - `[x]`: (선택) 팰의 x 위치입니다. 기본값: 명령어를 실행한 플레이어 기준 위치.
        - `[y]`: (선택) 팰의 y 위치입니다. 기본값: 명령어를 실행한 플레이어 기준 위치.
        - `[z]`: (선택) 팰의 z 위치입니다. 기본값: 명령어를 실행한 플레이어 기준 위치.
        - `[Level]`: (선택) 팰 레벨입니다. 기본값: 1.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /spawnpal Anubis 255
        ```
        _레벨 255 아누비스를 생성합니다!_

    ??? info "/spawnpal_ex"
        **문법:** `/spawnpal`과 같습니다.

        **설명:** `/spawnpal`과 같은 방식으로 팰을 생성하되 피해량 집계를 켭니다. 팰이 죽거나 포획되면 전체 피해량 순위를 로그에 기록하고, 웹훅이 설정되어 있으면 `PalWebhooks.webhookURL_Summons`로 전송합니다. `announceAdminSummonsKill`을 켜면 접속 중인 참가자에게 상위 5명과 자신의 순위가 표시된 결과 창도 보냅니다. 가장 많은 피해를 준 플레이어를 승자로 표시합니다. PalTemplate이나 PalSummon 파일을 사용하지 않으며 보상을 지급하지 않습니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /spawnpal_ex Anubis 230 -486 4097 80
        ```

    ??? info "/spawnnpc"
        **문법:** `/spawnnpc <NPCID|CharacterID> [Level=1]` 또는 `/spawnnpc <NPCID|CharacterID> <X> <Y> [Z] [Level=1]`

        **설명:** AI가 있는 NPC를 생성합니다. 채팅에서 좌표를 생략하면 관리자 근처에 생성하며, RCON에서는 좌표를 지정해야 합니다. `X`와 `Y`만 지정하면 지면 높이를 자동으로 찾습니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /spawnnpc PIDF_Soldier_AssaultRifle 30
        ```

    ??? info "/spawnpal_j"
        **문법:**

        다음 형식을 사용할 수 있습니다:

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal_j <PalTemplate> [x] [y] [z]`

        **설명:** 실행자 기준 위치 또는 지정한 절대 좌표에 팰을 생성합니다. **RCON에서는 x, y, z를 반드시 지정해야 합니다!**

        **참고:** `/givepal_j` 및 템플릿 기반 알 명령어와 마찬가지로 `Pals/Templates/`의 [PalTemplate](../FileTypes/PalTemplate.md) 속성을 사용합니다. 생성 옵션과 보상을 포함한 전투 이벤트에는 [PalSummon](../FileTypes/PalSummon.md) 파일을 사용하는 `/summon`을 실행하세요. `/spawnpal`은 템플릿 파일 이름이 아니라 팰 ID를 받습니다.

        **인수:**

        - `<PalTemplate>`: 사용할 [PalTemplate](../FileTypes/PalTemplate.md) 파일 이름입니다.
        - `[x]`: (선택) 팰의 x 위치입니다. 기본값: 명령어를 실행한 플레이어 기준 위치.
        - `[y]`: (선택) 팰의 y 위치입니다. 기본값: 명령어를 실행한 플레이어 기준 위치.
        - `[z]`: (선택) 팰의 z 위치입니다. 기본값: 명령어를 실행한 플레이어 기준 위치.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /spawnpal_j ArenaBoss 230 -486 4097
        ```

    ??? info "/spawnpal_ex_j"
        **문법:** `/spawnpal_ex_j <PalTemplate> [x] [y] [z]`

        **설명:** `/spawnpal_j`와 동일한 [PalTemplate](../FileTypes/PalTemplate.md) 및 좌표 처리 방식을 사용하되 피해량 집계를 켭니다. 팰이 죽거나 포획되면 전체 피해량 순위를 로그에 기록하고, 웹훅이 설정되어 있으면 `PalWebhooks.webhookURL_Summons`로 전송합니다. `announceAdminSummonsKill`을 켜면 접속 중인 참가자에게 상위 5명과 자신의 순위가 표시된 결과 창도 보냅니다. 가장 많은 피해를 준 플레이어를 승자로 표시합니다. [PalSummon](../FileTypes/PalSummon.md) 보상은 사용하지 않습니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /spawnpal_ex_j ArenaBoss 230 -486 4097
        ```

    ??? info "/summon"
        **문법:** `/summon <PalSummon>`

        **설명:** 지정한 [PalSummon](../FileTypes/PalSummon.md) 파일로 팰을 생성합니다.

        **참고:** 파일 이름에 .json 확장자를 넣지 않아도 됩니다. 생략하면 자동으로 추가합니다.

        **인수:**
        - `<PalSummon>`: `PalDefender/Pals/Summons/`의 [PalSummon](../FileTypes/PalSummon.md) 파일 이름입니다. [PalTemplate](../FileTypes/PalTemplate.md) 파일 이름을 지정하면 **안 됩니다**. 이 파일은 팰 속성용 PalTemplate을 참조하고 좌표 및 선택적인 보상 등의 생성 옵션을 추가합니다. 예를 들어 `/summon ArenaEncounter`는 `Pals/Summons/ArenaEncounter.json`을 불러옵니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **문법:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **설명:** 대상 사용자에게 지정한 팰이 들어 있는 알을 지급합니다. 레벨을 조정할 수 있습니다.

        **인수:**

        ??? quote "<UserId\>"
            **설명:** 알을 받을 플레이어 ID입니다.

        ??? quote "<EggId\>"
            **설명:** 지급할 알 유형입니다.

            **참고:** 각 유형에서 01(가장 작음)부터 05(가장 큼)까지 사용할 수 있습니다:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **설명:** 알 안에 들어갈 팰입니다.

            **참고:** `WeaselDragon`(칠렛)처럼 팰 ID를 사용하세요. 전체 목록은 [paldeck.cc/pals](https://paldeck.cc/pals)에서 확인할 수 있습니다.

        ??? quote "[Level\]"
            **설명:** (선택) 알 안의 팰 레벨입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **문법:** `/givemeegg <EggId> <PalId> [Level]`

        **설명:** 자신에게 지정한 팰이 들어 있는 알을 지급합니다. 레벨을 조정할 수 있습니다.

        **인수:**

        ??? quote "<EggId\>"
            **설명:** 자신에게 지급할 알 유형입니다.

            **참고:** 각 유형에서 01(가장 작음)부터 05(가장 큼)까지 사용할 수 있습니다:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **설명:** 알 안에 들어갈 팰입니다.

            **참고:** `WeaselDragon`(칠렛)처럼 팰 ID를 사용하세요. 전체 목록은 [paldeck.cc/pals](https://paldeck.cc/pals)에서 확인할 수 있습니다.

        ??? quote "[Level]"
            **설명:** (선택) 알 안의 팰 레벨입니다.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **문법:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **설명:** [PalTemplate](../FileTypes/PalTemplate.md) 파일에 정의된 팰이 들어 있는 알을 지급합니다. 레벨을 조정할 수 있습니다.

        **인수:**

        ??? quote "<EggId\>"
            **설명:** 지급할 알 유형입니다.

            **참고:** 각 유형에서 01(가장 작음)부터 05(가장 큼)까지 사용할 수 있습니다:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **설명:** 사용할 [PalTemplate](../FileTypes/PalTemplate.md) 파일 이름입니다.

            **참고:** 파일 이름에 .json 확장자를 넣지 않아도 됩니다. 생략하면 자동으로 추가합니다. [PalTemplate](../FileTypes/PalTemplate.md)을 참고하세요.

        ??? quote "[Level]"
            **설명:** (선택) 알 안의 팰 레벨입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **문법:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **설명:** 자신에게 [PalTemplate](../FileTypes/PalTemplate.md) 파일에 정의된 팰이 들어 있는 알을 지급합니다. 레벨을 조정할 수 있습니다.

        **인수:**

        ??? quote "<EggI\>"
            **설명:** 자신에게 지급할 알 유형입니다.

            **참고:** 각 유형에서 01(가장 작음)부터 05(가장 큼)까지 사용할 수 있습니다:

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **설명:** 사용할 [PalTemplate](../FileTypes/PalTemplate.md) 파일 이름입니다.

            **참고:** 파일 이름에 .json 확장자를 넣지 않아도 됩니다. 생략하면 자동으로 추가합니다. [PalTemplate](../FileTypes/PalTemplate.md)을 참고하세요.

        ??? quote "[Level]"
            **설명:** (선택) 알 안의 팰 레벨입니다.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **문법:** `/jetragon`

        **설명:** 관리자용 제트래곤을 지급합니다(정말 빠르… 벌써 사라졌네요).

        **인수:**
        - 없음

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **문법:** `/catwaifu`

        **설명:** 캐릭터 능력치를 강화하는 관리자용 Cat-Waifu를 지급합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **문법:** `/exportpals [UserId]`

        **설명:** 플레이어의 모든 팰을 Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/에 [PalTemplate](../FileTypes/PalTemplate.md) 파일로 내보냅니다.

        **인수:**

        - `[UserId]`: (선택) 팰을 내보낼 플레이어 ID입니다. 생략하면 자신의 팰을 내보냅니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **문법:** `/deletepals <UserId> <PalFilter>`

        **설명:** 고급 필터로 지정한 사용자의 팰을 삭제합니다. 한 명령어에서 팰 ID, 레벨, 성별, 패시브 등의 조건을 함께 지정할 수 있습니다. 중요한 데이터에 사용하기 전에 안전한 환경에서 테스트하세요.

        **인수:**

        ??? quote "<UserId\>"
            **설명:** 팰을 삭제할 플레이어 ID입니다.

        ??? quote "<PalFilter\>"
            **설명:** 삭제할 팰을 선택하는 필터 키워드 집합입니다.

            **참고:** 한 명령어에서 여러 키워드를 조합할 수 있습니다.

            사용 가능한 필터 키워드:

            - `ID`: PalID 또는 쉼표로 구분한 PalID 목록
            - `Nick`: 문자열(팰 이름)
            - `Gender`: `male`(수컷) 또는 `female`(암컷)
            - `Level`: 숫자. 지원하는 연산자: `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank`: 숫자. 지원하는 연산자: `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky`: `true` 또는 `false`(희귀 여부)
            - `Passives`: PassiveSkill 또는 쉼표로 구분한 PassiveSkill 목록
            - `Limit`: 숫자(삭제할 팰의 최대 수)

            **필터 예제:**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            위 필터 키와 예제는 현재 PalFilter의 참조 자료입니다.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "기술 트리"
    ??? info "/learntech"
        **문법:** `/learntech <UserId> <TechID>`

        **설명:** 플레이어에게 특정 기술을 습득시킵니다. 모두 해금하려면 `all`을 사용하세요.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<TechID>`: 습득할 기술입니다. 모두 해금하려면 `all`을 사용하세요.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **문법:** `/unlearntech <UserId> <TechID>`

        **설명:** 플레이어에게서 특정 기술을 제거합니다. 모두 제거하려면 `all`을 사용하세요.

        **인수:**

        - `<UserId>`: 플레이어 ID입니다.
        - `<TechID>`: 제거할 기술입니다. 모두 제거하려면 `all`을 사용하세요.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **문법:** `/givetechpoints <UserId> [Amount=1]`

        **설명:** 대상 사용자에게 지정한 양의 기술 포인트를 지급합니다.

        **인수:**

        - `<UserId>`: 기술 포인트를 받을 플레이어 ID입니다.
        - `[Amount]`: (선택) 지급할 기술 포인트입니다. 기본값: 1.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **문법:** `/givebosstechpoints <UserId> [Amount=1]`

        **설명:** 대상 사용자에게 지정한 양의 고대 기술 포인트를 지급합니다.

        **인수:**

        - `<UserId>`: 고대 기술 포인트를 받을 플레이어 ID입니다.
        - `[Amount]`: (선택) 지급할 고대 기술 포인트입니다. 기본값: 1.

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **문법:** `/givemetechpoints [Amount=1]`

        **설명:** 자신에게 지정한 양의 기술 포인트를 지급합니다.

        **인수:**

        - `[Amount]`: (선택) 자신에게 지급할 기술 포인트입니다. 기본값: 1.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **문법:** `/givemebosstechpoints [Amount=1]`

        **설명:** 자신에게 지정한 양의 고대 기술 포인트를 지급합니다.

        **인수:**

        - `[Amount]`: (선택) 자신에게 지급할 고대 기술 포인트입니다. 기본값: 1.

        **사용 조건:** `Chat`, `Admin`

        **예제:**
        ```
        /givemebosstechpoints 5
        ```


??? note "데이터 추출"
    ??? info "/gettechids"
        **문법:** `/gettechids`

        **설명:** 사용 가능한 모든 기술 ID를 반환합니다. RCON에서는 JSON을 반환합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **문법:** `/getskinids`

        **설명:** 사용 가능한 모든 팰 스킨 ID를 반환합니다. RCON에서는 JSON을 반환합니다.

        **인수:**

        - 없음

        **사용 조건:** `Chat`, `RCON`, `Admin`

        **예제:**
        ```
        /getskinids
        ```
