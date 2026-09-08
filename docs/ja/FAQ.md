# よくある質問

<details><summary style="font-size:16px">誤って自分自身または誰かを禁止してしまいました。どうすれば禁止を解除できますか?</summary>

<p style="font-size:14px">
アカウントの BAN 解除には <span class="var-command">/unban &lt;UserId&gt;</span>、IP BAN の解除には <span class="var-command">/unbanip &lt;IP&gt;</span> を使用します。PalDefender の BAN 情報は <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span> に保存されます。ファイルを手動で編集する場合は、先にサーバーを停止するか、編集後に設定を再読み込みしてください。
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>非推奨</span> Config.json を使用した旧 IP BAN の解除</summary>

<p style="font-size:14px">
古い Wiki では、<span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> から IP BAN を削除するよう案内していましたが、現在この方法は非推奨です。代わりに <span class="var-command">/unbanip &lt;IP&gt;</span> を使用するか、<span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span> を編集してください。
</p>

</details>


<details><summary style="font-size:16px">PalTemplate または PalSummon ファイルを追加または変更しましたが、コマンドが失敗しました。</summary>

<ul>
  <li>ファイルが有効な JSON であることを確認し、コメントと末尾のカンマを削除してください。</li>
  <li>テンプレートは <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span> に保存します。</li>
  <li>召喚ファイルは <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span> に保存します。</li>
  <li>パスを含めずにファイル名を指定します。例: <span class="var-command">/summon ArenaBoss</span></li>
  <li>召喚ファイルには <code>PalTemplate</code>、<code>X</code>、<code>Y</code>、<code>Z</code> が存在することを確認してください。</li>
  <li>テンプレート ファイルの場合は、<code>PalID</code> が存在し、有効な Pal ID を使用していることを確認してください。</li>
</ul>

</details>


<details><summary style="font-size:16px">コマンドにはどの ID を使用すればよいですか: UserId、PlayerUId、名前、または SteamID?</summary>

<p>
ほとんどの管理コマンドでは、<code>steam_...</code> や <code>gdk_...</code> など、プレーヤーの UserId が必要です。ゲーム内で <span class="var-command">/iwantplayerlist</span> を使用してプレイヤー リストに ID を表示するか、REST/API ツールを有効にしている場合はそれを使用します。
</p>

</details>


<details><summary style="font-size:16px">RCON では、チャット内でそれらがなくても機能するコマンドに座標または UserId が必要なのはなぜですか?</summary>

<p>
RCON にはゲーム内プレイヤー キャラクターが存在しないため、PalDefender はあなたの位置やターゲットを推測できません。 <span class="var-command">/getpos</span>、<span class="var-command">/tp</span>、<span class="var-command">/spawnpal</span> などのコマンド、およびベース位置コマンドの場合は、ターゲット プレーヤーまたは座標を明示的に指定します。
</p>

</details>


<details><summary style="font-size:16px">REST API は 401 または 403 を返します。何を確認すればよいですか?</summary>

<ul>
  <li><strong>401</strong>: <code>Authorization: Bearer &lt;token&gt;</code> ヘッダーを確認し、トークンファイルの名前が <code>TokenExample.json</code> ではないことを確認してください。</li>
  <li><strong>403</strong>: トークンのアクセス許可をチェックし、サーバーが起動を完了していることを確認してください。</li>
  <li>トークンを変更した後、サーバーを再起動するか、ホストのワークフローに従って API/トークンのセットアップを再ロードします。</li>
</ul>

</details>



<details><summary style="font-size:16px">管理者としてログインできません。管理コマンドはホワイトリストで保護されていると言われます。</summary>

<p>
次のように、IP を <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> に追加していることを確認してください。
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
あるいは、<span class="config-value">useAdminWhitelist</span> を <span class="var-bool">false</span> に設定することもできますが、チーターは管理者パスワードを取得するために何らかの悪用を行うことが知られているため、これはお勧めできません。
</p>

</details>



<details><summary style="font-size:16px">サーバーが起動時にクラッシュします。</summary>
<ul>
  <li>PalDefender が実行中の唯一の MOD であることを確認してください。他のすべての MOD を削除して、問題が解決しないかどうかを確認してください。</li>
  <li>PalDefender が最新バージョンであるかどうかを確認してください。</li>
  <li>お知らせについては、<a href="https://discord.gg/paldefender" target="_blank">discord</a>をご覧ください。</li>
  <li><span class="path">../Pal/Binaries/Win64/</span> の `PalDefender` ディレクトリの名前を変更し、サーバーを再起動します。</li>
  <li>場合によっては、<a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ 再頒布可能パッケージ</a> をインストールすると役に立ちます。</li>
</ul>

</details>


<details><summary style="font-size:16px">サーバー コンソールで特定のシンボルが正しく表示されません。</summary>

<p>
デフォルトの Windows コンソールの代わりに、Windows ターミナル (または適切な Unicode サポートを備えた代替ターミナル) を使用してください。
</p>

</details>



<details><summary style="font-size:16px">クラッシュを報告するにはどうすればよいですか?</summary>

<p>
<a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">問題セクション</a>で次のファイルを送信します。
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span></li>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span></li>
</ul>
</p>

<p>
目についた情報、またはその原因である可能性があると思われる情報はすべて削除してください。 PalDefender バージョンを忘れないでください。どのような情報も貴重なものになる可能性があります！
</p>

</details>
