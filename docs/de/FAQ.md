# FAQ

<details><summary style="font-size:16px">Ich habe mich/jemanden versehentlich gebannt. Wie kann ich den Bann aufheben?</summary>

<p style="font-size:14px">
Nutze <span class="var-command">/unban &lt;UserId&gt;</span> für Account-Banns und <span class="var-command">/unbanip &lt;IP&gt;</span> für IP-Banns. PalDefender speichert Bann-Einträge in <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>. Wenn du die Datei manuell bearbeitest, stoppe zuerst den Server oder lade die Konfiguration danach neu.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>Veraltet</span> Alte IP-Bann-Bereinigung über Config.json</summary>

<p style="font-size:14px">
Ältere Wiki-Versionen haben Admins angewiesen, IP-Banns aus <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> zu entfernen. Dieser Speicherort ist für Bann-Einträge veraltet. Nutze stattdessen <span class="var-command">/unbanip &lt;IP&gt;</span> oder bearbeite <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>.
</p>

</details>


<details><summary style="font-size:16px">Ich habe eine PalTemplate- oder PalSummon-Datei hinzugefuegt/geaendert, aber der Befehl schlaegt fehl.</summary>

<ul>
  <li>Stelle sicher, dass die Datei gültiges JSON ist. Entferne Kommentare und nachgestellte Kommas.</li>
  <li>Templates gehoeren nach <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>Summons gehoeren nach <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>Nutze den Dateinamen ohne Pfad, zum Beispiel <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>Prüfe bei Summon-Dateien, dass <code>PalTemplate</code>, <code>X</code>, <code>Y</code> und <code>Z</code> vorhanden sind.</li>
  <li>Prüfe bei Template-Dateien, dass <code>PalID</code> vorhanden ist und eine gültige Pal-ID verwendet.</li>
</ul>

</details>


<details><summary style="font-size:16px">Welche ID soll ich für Befehle verwenden: UserId, PlayerUId, Name oder SteamID?</summary>

<p>
Die meisten Admin-Befehle erwarten die UserId des Spielers, zum Beispiel <code>steam_...</code> oder <code>gdk_...</code>. Nutze im Spiel <span class="var-command">/iwantplayerlist</span>, um IDs in der Spielerliste anzuzeigen, oder nutze REST/API-Werkzeuge, wenn sie aktiviert sind.
</p>

</details>


<details><summary style="font-size:16px">Warum braucht RCON Koordinaten oder eine UserId für Befehle, die im Chat ohne funktionieren?</summary>

<p>
RCON hat keinen Spielercharakter im Spiel, daher kann PalDefender deine Position oder dein Ziel nicht ableiten. Gib bei Befehlen wie <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span> und Basispositions-Befehlen den Zielspieler oder die Koordinaten explizit an.
</p>

</details>


<details><summary style="font-size:16px">Die REST API gibt 401 oder 403 zurück. Was soll ich prüfen?</summary>

<ul>
  <li><strong>401</strong>: Prüfe den Header <code>Authorization: Bearer &lt;token&gt;</code> und stelle sicher, dass die Token-Datei nicht <code>TokenExample.json</code> heißt.</li>
  <li><strong>403</strong>: Prüfe die Token-Berechtigungen und stelle sicher, dass der Server vollständig gestartet ist.</li>
  <li>Starte den Server nach Token-Aenderungen neu oder lade die API-/Token-Einrichtung passend zu deinem Hosting-Workflow neu.</li>
</ul>

</details>



<details><summary style="font-size:16px">Ich kann mich nicht als Admin einloggen, weil Admin-Befehle durch die Whitelist geschuetzt sind.</summary>

<p>
Stelle sicher, dass du deine IP so in <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> eingetragen hast:
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
Alternativ kannst du <span class="config-value">useAdminWhitelist</span> auf <span class="var-bool">false</span> setzen. Das wird aber nicht empfohlen, da Cheater bekanntermassen Wege haben, an das Admin-Passwort zu gelangen.
</p>

</details>



<details><summary style="font-size:16px">Mein Server stuerzt beim Start ab.</summary>
<ul>
  <li>Stelle sicher, dass PalDefender der einzige aktive Mod ist. Entferne alle anderen Mods und pruefe, ob das Problem bestehen bleibt.</li>
  <li>Prüfe, ob PalDefender auf der neuesten Version ist.</li>
  <li>Prüfe unseren <a href="https://discord.gg/paldefender" target="_blank">Discord</a> auf Ankündigungen.</li>
  <li>Benenne den Ordner `PalDefender` in <span class="path">../Pal/Binaries/Win64/</span> um und starte den Server neu.</li>
  <li>In manchen Faellen hilft die Installation des <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ Redistributable</a>.</li>
</ul>

</details>


<details><summary style="font-size:16px">Ich sehe bestimmte Zeichen in meiner Serverkonsole nicht richtig.</summary>

<p>
Nutze bitte Windows Terminal oder eine Alternative mit guter Unicode-Unterstuetzung statt der Standard-Windows-Konsole.
</p>

</details>



<details><summary style="font-size:16px">Wie kann ich Abstuerze melden?</summary>

<p>
Sende folgende Dateien im <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">Issue-Bereich</a>:
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span>
</ul>
</p>

<p>
Fuege alle Informationen hinzu, die du gesehen hast oder als Ursache vermutest. Vergiss die PalDefender-Version nicht! Jede Information kann wertvoll sein!
</p>

</details>
