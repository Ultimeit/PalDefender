# 常见问题

<details><summary style="font-size:16px">我不小心封禁了自己/某人。如何解封他们？</summary>

<p style="font-size:14px">
如果您封禁了他们的 IP，目前您需要编辑 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> 文件，然后重新加载配置（<span class="var-command">/reloadcfg</span>）或重启服务器。如果您封禁了他们的账户，您需要从 <span class="path-partial">../Pal/Saved/SaveGames/</span><span class="file-partial">banlist.txt</span> 中删除他们的 UserId，然后重启服务器。
</p>

</details>



<details><summary style="font-size:16px">我无法以管理员身份登录，提示管理员命令受白名单保护。</summary>

<p>
请确保您已将您的 IP 添加到 <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>，如下所示：
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
或者，您可以将 <span class="config-value">useAdminWhitelist</span> 设置为 <span class="var-bool">false</span>，但不推荐这样做，因为已知作弊者可以通过某种漏洞利用来获取管理员密码。
</p>

</details>



<details><summary style="font-size:16px">我的服务器在启动时崩溃。</summary>
<ul>
  <li>确保 PalDefender 是唯一运行的模组 - 删除所有其他模组，看看问题是否仍然存在。</li>
  <li>检查 PalDefender 是否为最新版本。</li>
  <li>查看我们的 <a href="https://discord.gg/paldefender" target="_blank">discord</a> 以获取任何公告。</li>
  <li>重命名 <span class="path">../Pal/Binaries/Win64/</span> 中的 `PalDefender` 目录并重启服务器。</li>
  <li>在某些情况下，安装 <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ 运行库</a> 可能会有所帮助。</li>
</ul>

</details>


<details><summary style="font-size:16px">我在服务器控制台中无法正确看到某些符号。</summary>

<p>
请使用 Windows Terminal（或任何支持 unicode 的替代方案）而不是默认的 Windows 控制台。
</p>

</details>



<details><summary style="font-size:16px">如何报告崩溃？</summary>

<p>
在 <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">问题部分</a> 发送以下文件：
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;随机数字&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;最近的日志&gt;</span>
</ul>
</p>

<p>
请确保提供您能看到或推测的任何可能原因的信息。不要忘记 PalDefender 版本！任何信息都可能很有价值！
</p>

</details>

