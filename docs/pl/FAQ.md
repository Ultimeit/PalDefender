# Często zadawane pytania

<details><summary style="font-size:16px">Przez pomyłkę zbanowałem siebie lub inną osobę. Jak usunąć bana?</summary>

<p style="font-size:14px">
Bana konta usuń poleceniem <span class="var-command">/unban &lt;UserId&gt;</span>, a blokadę IP — <span class="var-command">/unbanip &lt;IP&gt;</span>. PalDefender zapisuje bany w <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>. Przed ręczną edycją zatrzymaj serwer albo po edycji ponownie wczytaj konfigurację.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>Przestarzałe</span> Dawne usuwanie blokad IP przez Config.json</summary>

<p style="font-size:14px">
Starsze wersje wiki zalecały usuwanie blokad IP z <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>. Ten plik nie służy już do przechowywania banów. Użyj <span class="var-command">/unbanip &lt;IP&gt;</span> lub edytuj <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>.
</p>

</details>


<details><summary style="font-size:16px">Dodałem lub zmieniłem plik PalTemplate albo PalSummon, ale polecenie nie działa.</summary>

<ul>
  <li>Upewnij się, że plik zawiera prawidłowy JSON. Usuń komentarze i przecinki po ostatnich elementach.</li>
  <li>Szablony umieść w <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>Pliki przywołań umieść w <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>Podaj samą nazwę pliku, bez ścieżki, np. <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>W plikach przywołań sprawdź obecność pól <code>PalTemplate</code>, <code>X</code>, <code>Y</code> i <code>Z</code>.</li>
  <li>W szablonach sprawdź, czy pole <code>PalID</code> istnieje i zawiera prawidłowy identyfikator Pala.</li>
</ul>

</details>


<details><summary style="font-size:16px">Którego identyfikatora używać w poleceniach: UserId, PlayerUId, nazwy czy SteamID?</summary>

<p>
Większość poleceń administratora wymaga UserId gracza, np. <code>steam_...</code> lub <code>gdk_...</code>. Polecenie <span class="var-command">/iwantplayerlist</span> w grze pokazuje identyfikatory na liście graczy. Jeśli REST API jest włączone, możesz też skorzystać z narzędzi API.
</p>

</details>


<details><summary style="font-size:16px">Dlaczego RCON wymaga współrzędnych lub UserId w poleceniach, które działają bez nich na czacie?</summary>

<p>
RCON nie ma postaci w grze, więc PalDefender nie może określić Twojej pozycji ani celu. W poleceniach takich jak <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span> oraz poleceniach dotyczących położenia baz podaj wprost docelowego gracza lub współrzędne.
</p>

</details>


<details><summary style="font-size:16px">REST API zwraca 401 lub 403. Co sprawdzić?</summary>

<ul>
  <li><strong>401</strong>: Sprawdź nagłówek <code>Authorization: Bearer &lt;token&gt;</code> i upewnij się, że plik tokena nie nazywa się <code>TokenExample.json</code>.</li>
  <li><strong>403</strong>: Sprawdź uprawnienia tokena i upewnij się, że serwer zakończył uruchamianie.</li>
  <li>Po zmianie tokenów uruchom ponownie serwer lub wczytaj ponownie ustawienia API/tokenów zgodnie z procedurą Twojego hostingu.</li>
</ul>

</details>



<details><summary style="font-size:16px">Nie mogę zalogować się jako administrator. Pojawia się informacja, że polecenia administratora są chronione listą dozwolonych adresów.</summary>

<p>
Upewnij się, że Twój adres IP jest dodany do <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>, np. tak:
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
Możesz też ustawić <span class="config-value">useAdminWhitelist</span> na <span class="var-bool">false</span>, ale nie jest to zalecane: znane są sposoby wykorzystania błędów gry do uzyskania hasła administratora.
</p>

</details>



<details><summary style="font-size:16px">Mój serwer ulega awarii podczas uruchamiania.</summary>
<ul>
  <li>Sprawdź, czy problem występuje, gdy PalDefender jest jedynym uruchomionym modem. Usuń pozostałe mody i spróbuj ponownie.</li>
  <li>Sprawdź, czy używasz najnowszej wersji PalDefender.</li>
  <li>Sprawdź ogłoszenia na naszym <a href="https://discord.gg/paldefender" target="_blank">Discordzie</a>.</li>
  <li>Zmień nazwę katalogu `PalDefender` w <span class="path">../Pal/Binaries/Win64/</span> i uruchom serwer ponownie.</li>
  <li>W niektórych przypadkach pomaga instalacja <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">pakietu redystrybucyjnego VC++</a>.</li>
</ul>

</details>


<details><summary style="font-size:16px">Niektóre znaki wyświetlają się nieprawidłowo w konsoli serwera.</summary>

<p>
Użyj Windows Terminal lub innego terminala z poprawną obsługą Unicode zamiast domyślnej konsoli Windows.
</p>

</details>



<details><summary style="font-size:16px">Jak zgłaszać awarie?</summary>

<p>
Dołącz poniższe pliki do zgłoszenia w <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">sekcji Issues</a>:
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;losowe liczby&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;najnowsze logi&gt;</span>
</ul>
</p>

<p>
Opisz zaobserwowane objawy i możliwe przyczyny. Nie zapomnij podać wersji PalDefender! Każda informacja może pomóc w rozwiązaniu problemu.
</p>

</details>

