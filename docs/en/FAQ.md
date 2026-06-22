# FAQ

<details><summary style="font-size:16px"><span class='pd-badge pd-badge--beta'>Beta</span> I've accidentally banned myself/someone. How can I unban them?</summary>

<p style="font-size:14px">
Use <span class="var-command">/unban &lt;UserId&gt;</span> for account bans and <span class="var-command">/unbanip &lt;IP&gt;</span> for IP bans. PalDefender ban records are stored in <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>. If you edit the file manually, stop the server first or reload configuration after editing.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>Deprecated</span> Old IP-ban cleanup through Config.json</summary>

<p style="font-size:14px">
Older wiki versions told admins to remove IP bans from <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>. That path is deprecated for ban records. Use <span class="var-command">/unbanip &lt;IP&gt;</span> or edit <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span> instead.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--beta'>Beta</span>: I added or changed a PalTemplate or PalSummon file but the command fails.</summary>

<ul>
  <li>Make sure the file is valid JSON. Remove comments and trailing commas.</li>
  <li>Templates belong in <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>Summons belong in <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>Use the filename without path, for example <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>For summon files, check that <code>PalTemplate</code>, <code>X</code>, <code>Y</code>, and <code>Z</code> are present.</li>
  <li>For template files, check that <code>PalID</code> is present and uses a valid Pal ID.</li>
</ul>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--beta'>Beta</span>: Which ID should I use for commands: UserId, PlayerUId, name, or SteamID?</summary>

<p>
Most admin commands expect the player's UserId, such as <code>steam_...</code> or <code>gdk_...</code>. Use <span class="var-command">/iwantplayerlist</span> in-game to show IDs in the player list, or use REST/API tooling if you have it enabled.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--beta'>Beta</span>: Why does RCON require coordinates or a UserId for commands that work without them in chat?</summary>

<p>
RCON has no in-game player character, so PalDefender cannot infer your position or target. For commands like <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span>, and base-location commands, provide the target player or coordinates explicitly.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--beta'>Beta</span>: The REST API returns 401 or 403. What should I check?</summary>

<ul>
  <li><strong>401</strong>: Check the <code>Authorization: Bearer &lt;token&gt;</code> header and make sure the token file is not named <code>TokenExample.json</code>.</li>
  <li><strong>403</strong>: Check token permissions and make sure the server has finished starting.</li>
  <li>After changing tokens, restart the server or reload the API/token setup according to your host workflow.</li>
</ul>

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

