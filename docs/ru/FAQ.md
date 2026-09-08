# Часто задаваемые вопросы

<details><summary style="font-size:16px">Я случайно заблокировал myself/someone. Как мне разбанить его?</summary>

<p style="font-size:14px">
Используйте <span class="var-command">/unban &lt;UserId&gt;</span> для блокировки учетных записей и <span class="var-command">/unbanip &lt;IP&gt;</span> для блокировки IP-адресов. Записи о банах PalDefender хранятся в <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>. Если вы редактируете файл вручную, сначала остановите сервер или перезагрузите конфигурацию после редактирования.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>Deprecated</span> Очистка старого IP-бана через Config.json</summary>

<p style="font-size:14px">
В старых версиях вики администраторам предлагалось снять блокировку IP-адресов с <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>. Этот путь устарел для записей о запрете. Вместо этого используйте <span class="var-command">/unbanip &lt;IP&gt;</span> или отредактируйте <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>.
</p>

</details>


<details><summary style="font-size:16px">Я добавил или изменил файл PalTemplate или PalSummon, но команда не выполнена.</summary>

<ul>
  <li>Убедитесь, что файл JSON действителен. Удалите комментарии и конечные запятые.</li>
  <li>Шаблоны принадлежат <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>Призывы относятся к <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>Используйте имя файла без пути, например <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>Для файлов призыва убедитесь, что присутствуют <code>PalTemplate</code>, <code>X</code>, <code>Y</code> и <code>Z</code>.</li>
  <li>Для файлов шаблонов убедитесь, что <code>PalID</code> присутствует и использует действительный идентификатор Pal.</li>
</ul>

</details>


<details><summary style="font-size:16px">Какой идентификатор следует использовать для команд: UserId, PlayerUId, имя или SteamID?</summary>

<p>
Большинство команд администратора ожидают UserId игрока, например <code>steam_...</code> или <code>gdk_...</code>. Используйте <span class="var-command">/iwantplayerlist</span> в игре, чтобы отображать идентификаторы в списке игроков, или используйте инструмент REST/API, если он у вас включен.
</p>

</details>


<details><summary style="font-size:16px">Почему RCON требует координаты или UserId для команд, которые работают без них в чате?</summary>

<p>
RCON не имеет внутриигрового персонажа, поэтому PalDefender не может определить вашу позицию или цель. Для таких команд, как <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span> и команд базового местоположения, явно укажите целевого игрока или его координаты.
</p>

</details>


<details><summary style="font-size:16px"> REST API возвращает 401 или 403. Что мне следует проверить?</summary>

<ul>
  <li><strong>401</strong>: проверьте заголовок <code>Authorization: Bearer &lt;token&gt;</code> и убедитесь, что файл токена не имеет имени <code>TokenExample.json</code>.</li>.
  <li><strong>403</strong>: проверьте разрешения токена и убедитесь, что запуск сервера завершен.</li>
  <li>После изменения токенов перезапустите сервер или перезагрузите настройку API/token в соответствии с рабочим процессом вашего хоста.</li>
</ul>

</details>



<details><summary style="font-size:16px">Я не могу войти в систему как администратор, пишет, что команды администратора защищены белым списком.</summary>

<p>
Убедитесь, что вы добавили свой IP-адрес в <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> следующим образом:
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
Альтернативно вы можете установить для <span class="config-value">useAdminWhitelist</span> значение <span class="var-bool">false</span>, но это не рекомендуется, поскольку известно, что у мошенников есть какой-то эксплойт для получения пароля администратора.
</p>

</details>



<details><summary style="font-size:16px">Мой сервер выходит из строя при запуске.</summary>
<ul>
  <li>Убедитесь, что PalDefender — единственный работающий мод: удалите все остальные моды и проверьте, сохраняется ли проблема.</li>
  <li>Проверьте, установлена ли PalDefender последней версии.</li>
  <li>Познакомьтесь с нашими объявлениями <a href="https://discord.gg/paldefender" target="_blank">discord</a>.</li>
  <li>Переименуйте каталог `PalDefender` в <span class="path">../Pal/Binaries/Win64/</span> и перезапустите сервер.</li>
  <li>В некоторых случаях может помочь установка распространяемого компонента <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++</a>.</li>
</ul>

</details>


<details><summary style="font-size:16px">Я не могу правильно видеть некоторые символы в консоли сервера.</summary>

<p>
Используйте терминал Windows (или любую альтернативу с надлежащей поддержкой Unicode) вместо консоли windows по умолчанию.
</p>

</details>



<details><summary style="font-size:16px">Как сообщить о сбоях?</summary>

<p>
Отправьте следующие файлы в раздел проблем <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank"></a>:
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span>
</ul>
</p>

<p>
Обязательно оставьте любую информацию, которую вы могли видеть или предположить, что это может быть причиной. Не забудьте версию PalDefender! Любая информация может быть ценной!
</p>

</details>

