# 자주 묻는 질문

<details><summary style="font-size:16px">실수로 자신이나 다른 사람을 차단했습니다. 어떻게 해제하나요?</summary>

<p style="font-size:14px">
계정 차단은 <span class="var-command">/unban &lt;UserId&gt;</span>으로, IP 차단은 <span class="var-command">/unbanip &lt;IP&gt;</span>로 해제하세요. PalDefender의 차단 기록은 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>에 저장됩니다. 파일을 직접 수정하려면 먼저 서버를 중지하거나, 수정 후 설정을 다시 불러오세요.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>사용 중단</span> Config.json에서 IP 차단을 해제하던 기존 방법</summary>

<p style="font-size:14px">
이전 위키에서는 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>에서 IP 차단 항목을 삭제하도록 안내했습니다. 이제 이 파일에서는 차단 기록을 관리하지 않습니다. <span class="var-command">/unbanip &lt;IP&gt;</span>를 사용하거나 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>을 수정하세요.
</p>

</details>


<details><summary style="font-size:16px">PalTemplate 또는 PalSummon 파일을 추가하거나 수정한 뒤 명령어가 실패합니다.</summary>

<ul>
  <li>파일이 올바른 JSON인지 확인하세요. 주석과 마지막 항목 뒤의 쉼표를 제거하세요.</li>
  <li>템플릿 파일은 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>에 넣으세요.</li>
  <li>소환 파일은 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>에 넣으세요.</li>
  <li>경로를 제외한 파일 이름을 사용하세요. 예: <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>소환 파일에 <code>PalTemplate</code>, <code>X</code>, <code>Y</code>, <code>Z</code>가 있는지 확인하세요.</li>
  <li>템플릿 파일에 <code>PalID</code>가 있고 유효한 팰 ID가 지정되어 있는지 확인하세요.</li>
</ul>

</details>


<details><summary style="font-size:16px">명령어에는 UserId, PlayerUId, 이름, SteamID 중 어떤 ID를 사용해야 하나요?</summary>

<p>
대부분의 관리자 명령어에는 <code>steam_...</code> 또는 <code>gdk_...</code> 형식의 UserId를 사용합니다. 게임 내에서 <span class="var-command">/iwantplayerlist</span>를 실행하면 플레이어 목록에 ID가 표시됩니다. REST API를 활성화했다면 관련 도구로도 확인할 수 있습니다.
</p>

</details>


<details><summary style="font-size:16px">채팅에서는 좌표나 UserId 없이 실행되는 명령어가 RCON에서는 왜 필요한가요?</summary>

<p>
RCON에는 게임 내 플레이어 캐릭터가 없으므로 PalDefender가 실행자의 위치나 대상을 알아낼 수 없습니다. <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span> 및 거점 위치 관련 명령어에는 대상 플레이어나 좌표를 직접 지정하세요.
</p>

</details>


<details><summary style="font-size:16px">REST API가 401 또는 403을 반환합니다. 무엇을 확인해야 하나요?</summary>

<ul>
  <li><strong>401</strong>: <code>Authorization: Bearer &lt;token&gt;</code> 헤더를 확인하고 토큰 파일 이름이 <code>TokenExample.json</code>이 아닌지 확인하세요.</li>
  <li><strong>403</strong>: 토큰 권한을 확인하고 서버 시작이 완료되었는지 확인하세요.</li>
  <li>토큰을 변경한 뒤에는 서버를 재시작하거나 호스팅 환경의 절차에 따라 API/토큰 설정을 다시 불러오세요.</li>
</ul>

</details>



<details><summary style="font-size:16px">관리자로 로그인할 수 없고 관리자 명령어가 허용 목록으로 보호된다는 메시지가 나옵니다.</summary>

<p>
다음과 같이 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>에 자신의 IP를 추가했는지 확인하세요.
</p>
```json
"useAdminWhitelist": true,
"adminIPs": [
    "127.0.0.1",
    "196.128.2.*",
    "123.222.111.122",
    "111.111.111.111",
],
```

<p>
<span class="config-value">useAdminWhitelist</span>를 <span class="var-bool">false</span>로 설정할 수도 있습니다. 하지만 관리자 비밀번호를 알아내는 취약점 악용 사례가 알려져 있으므로 권장하지 않습니다.
</p>

</details>



<details><summary style="font-size:16px">서버가 시작할 때 충돌합니다.</summary>
<ul>
  <li>PalDefender만 실행되는 상태에서 확인하세요. 다른 모드를 모두 제거한 뒤에도 문제가 발생하는지 확인하세요.</li>
  <li>PalDefender가 최신 버전인지 확인하세요.</li>
  <li><a href="https://discord.gg/paldefender" target="_blank">Discord</a>에서 공지사항을 확인하세요.</li>
  <li><span class="path">../Pal/Binaries/Win64/</span>의 `PalDefender` 디렉터리 이름을 변경한 뒤 서버를 재시작하세요.</li>
  <li>경우에 따라 <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ 재배포 가능 패키지</a> 설치가 도움이 될 수 있습니다.</li>
</ul>

</details>


<details><summary style="font-size:16px">서버 콘솔에서 일부 문자가 제대로 표시되지 않습니다.</summary>

<p>
기본 Windows 콘솔 대신 Windows Terminal이나 유니코드를 제대로 지원하는 다른 터미널을 사용하세요.
</p>

</details>



<details><summary style="font-size:16px">충돌은 어떻게 제보하나요?</summary>

<p>
다음 파일을 <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">이슈 게시판</a>에 첨부하세요.
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;임의의 숫자&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;최근 로그&gt;</span>
</ul>
</p>

<p>
확인한 현상이나 원인으로 의심되는 내용을 함께 적어 주세요. PalDefender 버전도 꼭 알려 주세요! 사소한 정보도 문제 해결에 도움이 될 수 있습니다.
</p>

</details>

