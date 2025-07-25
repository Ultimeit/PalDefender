# FAQ

<details><summary style="font-size:16px">I've accidentally banned myself/someone. How can I unban them?</summary>

<p style="font-size:14px">
If you've banned their IP, for the time being you would need to edit <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> file and either reload the config (<span class="var-command">/reloadcfg</span>) or restart the server. If you've banned their account, you would need to remove their UserId from <span class="path-partial">../Pal/Saved/SaveGames/</span><span class="file-partial">banlist.txt</span> and restart the server afterwards.
</p>

</details>



<details><summary style="font-size:16px">I cannot login as an admin, it says that admin commands are whitelist protected.</summary>

<p>
Make sure you have added your IP to <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> like this:
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
Alternatively, you can set <span class="config-value">useAdminWhitelist</span> to <span class="var-bool">false</span> but that is not recommended, since cheaters are known to have some kind of exploit to obtain admin password.
</p>

</details>



<details><summary style="font-size:16px">My server crashes on startup.</summary>
<ul>
  <li>Ensure PalDefender is the only one mod running - delete all other mods and see if the problem persists.</li>
  <li>Check if PalDefender is on the newest version.</li>
  <li>Check out our <a href="https://discord.gg/paldefender" target="_blank">discord</a> for any announcements.</li>
  <li>Rename `PalDefender` directory in <span class="path">../Pal/Binaries/Win64/</span> and restart the server.</li>
  <li>In certain cases installing <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ redistributable</a> can help.</li>
</ul>

</details>


<details><summary style="font-size:16px">I cannot see certain symbols properly in my server console.</summary>

<p>
Please use Windows Terminal (or any alternative with proper unicode support) instead of default windows console.
</p>

</details>



<details><summary style="font-size:16px">How can I report crashes?</summary>

<p>
Send following files in the <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">issue section</a>:
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span>
</ul>
</p>

<p>
Make sure to drop any information you could see or assume that might be the reason. Dont forget the PalDefender version! Any information can be valuable!
</p>

</details>

