# 常见问题

<details><summary style="font-size:16px">我不小心封禁了自己/其他人。如何解除封禁？</summary>

<p style="font-size:14px">
账号封禁请使用 <span class="var-command">/unban &lt;UserId&gt;</span>，IP 封禁请使用 <span class="var-command">/unbanip &lt;IP&gt;</span>。PalDefender 的封禁记录保存在 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>。如果要手动编辑该文件，请先停止服务器，或在编辑后重新加载配置。
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>已废弃</span> 旧版通过 Config.json 清理 IP 封禁</summary>

<p style="font-size:14px">
旧版 Wiki 曾提示管理员从 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> 删除 IP 封禁。该位置已不再用于封禁记录。请改用 <span class="var-command">/unbanip &lt;IP&gt;</span>，或编辑 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>。
</p>

</details>


<details><summary style="font-size:16px">我添加或修改了 PalTemplate/PalSummon 文件，但命令失败。</summary>

<ul>
  <li>确认文件是有效 JSON。请移除注释和末尾多余逗号。</li>
  <li>模板应放在 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>召唤文件应放在 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>使用不带路径的文件名，例如 <span class="var-command">/summon ArenaBoss</span>。</li>
  <li>对于召唤文件，请确认包含 <code>PalTemplate</code>、<code>X</code>、<code>Y</code> 和 <code>Z</code>。</li>
  <li>对于模板文件，请确认包含 <code>PalID</code>，并且使用有效的 Pal ID。</li>
</ul>

</details>


<details><summary style="font-size:16px">命令应该使用哪种 ID：UserId、PlayerUId、名称还是 SteamID？</summary>

<p>
大多数管理员命令需要玩家的 UserId，例如 <code>steam_...</code> 或 <code>gdk_...</code>。在游戏内使用 <span class="var-command">/iwantplayerlist</span> 可在玩家列表中显示 ID；如果已启用，也可以使用 REST/API 工具。
</p>

</details>


<details><summary style="font-size:16px">为什么在聊天中不需要参数的命令，通过 RCON 执行时需要坐标或 UserId？</summary>

<p>
RCON 没有游戏内玩家角色，因此 PalDefender 无法推断你的位置或目标。对于 <span class="var-command">/getpos</span>、<span class="var-command">/tp</span>、<span class="var-command">/spawnpal</span> 以及基地位置相关命令，请明确提供目标玩家或坐标。
</p>

</details>


<details><summary style="font-size:16px">REST API 返回 401 或 403，我应该检查什么？</summary>

<ul>
  <li><strong>401</strong>: 检查 <code>Authorization: Bearer &lt;token&gt;</code> 请求头，并确认令牌文件没有命名为 <code>TokenExample.json</code>。</li>
  <li><strong>403</strong>: 检查令牌权限，并确认服务器已经完成启动。</li>
  <li>修改令牌后，请根据你的主机流程重启服务器，或重新加载 API/令牌配置。</li>
</ul>

</details>



<details><summary style="font-size:16px">我无法以管理员身份登录，提示管理员命令受白名单保护。</summary>

<p>
请确认你已像这样把自己的 IP 添加到 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>：
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
也可以将 <span class="config-value">useAdminWhitelist</span> 设为 <span class="var-bool">false</span>，但不推荐这样做，因为已知作弊者可能通过漏洞获取管理员密码。
</p>

</details>



<details><summary style="font-size:16px">我的服务器启动时崩溃。</summary>
<ul>
  <li>确认 PalDefender 是唯一运行的 Mod。删除其他 Mod 后检查问题是否仍然存在。</li>
  <li>检查 PalDefender 是否为最新版本。</li>
  <li>查看我们的 <a href="https://discord.gg/paldefender" target="_blank">Discord</a> 了解公告。</li>
  <li>重命名 <span class="path">../Pal/Binaries/Win64/</span> 中的 `PalDefender` 目录，然后重启服务器。</li>
  <li>在某些情况下，安装 <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ Redistributable</a> 会有帮助。</li>
</ul>

</details>


<details><summary style="font-size:16px">我的服务器控制台无法正确显示某些符号。</summary>

<p>
请使用 Windows Terminal，或其他正确支持 Unicode 的终端，而不是默认 Windows 控制台。
</p>

</details>



<details><summary style="font-size:16px">如何报告崩溃？</summary>

<p>
请在 <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">Issue 区</a>发送以下文件：
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span>
</ul>
</p>

<p>
请附上你看到的、或认为可能相关的任何信息。不要忘记 PalDefender 版本！任何信息都可能有价值。
</p>

</details>

