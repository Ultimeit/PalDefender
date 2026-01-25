# FAQ

<details><summary style="font-size:16px">Ich habe mich selbst / jemanden aus Versehen gebannt. Wie kann ich die Sperre aufheben?</summary>

<p style="font-size:14px">
Wenn du die IP-Adresse gebannt hast, musst du vorübergehend die Datei
<span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> bearbeiten und anschließend entweder die Konfiguration neu laden (<span class="var-command">/reloadcfg</span>) oder den Server neu starten.
<br><br>
Wenn du den Account gebannt hast, entferne die entsprechende UserId aus der Datei
<span class="path-partial">../Pal/Saved/SaveGames/</span><span class="file-partial">banlist.txt</span> und starte den Server danach neu.
</p>

</details>



<details><summary style="font-size:16px">Ich kann mich nicht als Admin anmelden. Es wird angezeigt, dass Admin-Befehle durch eine Whitelist geschützt sind.</summary>

<p>
Stelle sicher, dass du deine IP-Adresse wie folgt in der Datei
<span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> hinzugefügt hast:
</p>

```json
"useAdminWhitelist": true,
"adminIPs": [
    "127.0.0.1",
    "196.128.2.*",
    "123.222.111.122",
    "111.111.111.111"
],
```
<p>
Alternativ kannst du <span class="config-value">useAdminWhitelist</span> auf <span class="var-bool">false</span> setzen. Dies wird jedoch <strong>nicht empfohlen</strong>, da bekannt ist, dass Cheater Exploits nutzen können, um an das Admin-Passwort zu gelangen.
</p>



</details><details><summary style="font-size:16px">Mein Server stürzt beim Start ab.</summary>
<ul>
  <li>Stelle sicher, dass PalDefender das <strong>einzige</strong> aktive Mod ist – entferne alle anderen Mods und prüfe, ob das Problem weiterhin besteht.</li>
  <li>Überprüfe, ob PalDefender auf dem neuesten Stand ist.</li>
  <li>Sieh in unserem <a href="https://discord.gg/paldefender" target="_blank">Discord</a> nach, ob es aktuelle Ankündigungen gibt.</li>
  <li>Benenne das Verzeichnis <code>PalDefender</code> unter <span class="path">../Pal/Binaries/Win64/</span> um und starte den Server neu.</li>
  <li>In manchen Fällen kann die Installation der <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ Redistributables</a> helfen.</li>
</ul></details>



<details><summary style="font-size:16px">Ich kann bestimmte Symbole in der Server-Konsole nicht korrekt sehen.</summary>

<p>
Bitte verwende das <strong>Windows Terminal</strong> (oder eine andere Konsole mit vollständiger Unicode-Unterstützung) anstelle der standardmäßigen Windows-Konsole.
</p>

</details>



<details><summary style="font-size:16px">Wie kann ich Abstürze melden?</summary>

<p>
Bitte sende die folgenden Dateien im <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">Issue-Bereich</a> ein:
</p>
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;zufällige Nummern&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span></li>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;aktuelle Logs&gt;</span></li>
</ul>
<p>
Gib bitte alle Informationen an, die dir aufgefallen sind oder die du als mögliche Ursache vermutest. Vergiss außerdem nicht, die verwendete <strong>PalDefender-Version</strong> anzugeben – jede Information kann hilfreich sein.
</p>
</details>

