# Perguntas frequentes

<details><summary style="font-size:16px">Bani acidentalmente myself/someone. Como posso cancelar o banimento?</summary>

<p style="font-size:14px">
Use <span class="var-command">/unban &lt;UserId&gt;</span> para banimentos de contas e <span class="var-command">/unbanip &lt;IP&gt;</span> para banimentos de IP. Os registros de banimento de PalDefender são armazenados em <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>. Se você editar o arquivo manualmente, pare o servidor primeiro ou recarregue a configuração após a edição.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>Deprecated</span> Limpeza de banimento de IP antigo por meio de Config.json</summary>

<p style="font-size:14px">
Versões mais antigas do wiki instruíam os administradores a remover os banimentos de IP de <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>. Esse caminho está obsoleto para registros de banimento. Use <span class="var-command">/unbanip &lt;IP&gt;</span> ou edite <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>.
</p>

</details>


<details><summary style="font-size:16px">Eu adicionei ou alterei um arquivo PalTemplate ou PalSummon, mas o comando falhou.</summary>

<ul>
  <li>Certifique-se de que o arquivo seja válido JSON. Remova comentários e vírgulas finais.</li>
  <li>Os modelos pertencem a <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>As convocações pertencem a <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>Use o nome do arquivo sem caminho, por exemplo <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>Para arquivos de convocação, verifique se <code>PalTemplate</code>, <code>X</code>, <code>Y</code> e <code>Z</code> estão presentes.</li>
  <li>Para arquivos de modelo, verifique se <code>PalID</code> está presente e usa um Pal ID válido.</li>
</ul>

</details>


<details><summary style="font-size:16px">Qual ID devo usar para comandos: UserId, PlayerUId, nome ou SteamID?</summary>

<p>
A maioria dos comandos administrativos espera o UserId do jogador, como <code>steam_...</code> ou <code>gdk_...</code>. Use <span class="var-command">/iwantplayerlist</span> no jogo para mostrar IDs na lista de jogadores ou use a ferramenta REST/API se estiver ativada.
</p>

</details>


<details><summary style="font-size:16px">Por que RCON requer coordenadas ou um UserId para comandos que funcionam sem elas no chat?</summary>

<p>
RCON não tem personagem de jogador no jogo, então PalDefender não pode inferir sua posição ou alvo. Para comandos como <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span> e comandos de localização base, forneça explicitamente o jogador alvo ou as coordenadas.
</p>

</details>


<details><summary style="font-size:16px">O REST API retorna 401 ou 403. O que devo verificar?</summary>

<ul>
  <li><strong>401</strong>: verifique o cabeçalho <code>Authorization: Bearer &lt;token&gt;</code> e certifique-se de que o arquivo de token não tenha o nome <code>TokenExample.json</code>.</li>
  <li><strong>403</strong>: Verifique as permissões do token e certifique-se de que o servidor terminou de iniciar.</li>
  <li>Após alterar os tokens, reinicie o servidor ou recarregue a configuração do API/token de acordo com o fluxo de trabalho do seu host.</li>
</ul>

</details>



<details><summary style="font-size:16px">Não consigo fazer login como administrador, isso diz que os comandos do administrador estão protegidos pela lista de permissões.</summary>

<p>
Certifique-se de ter adicionado seu IP a <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> assim:
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
Alternativamente, você pode definir <span class="config-value">useAdminWhitelist</span> como <span class="var-bool">false</span>, mas isso não é recomendado, pois sabe-se que os trapaceiros têm algum tipo de exploração para obter a senha do administrador.
</p>

</details>



<details><summary style="font-size:16px">Meu servidor falha na inicialização.</summary>
<ul>
  <li>Certifique-se de que o PalDefender seja o único mod em execução — remova todos os outros mods e veja se o problema persiste.</li>
  <li>Verifique se PalDefender está na versão mais recente.</li>
  <li>Confira nosso <a href="https://discord.gg/paldefender" target="_blank">discord</a> para quaisquer anúncios.</li>
  <li>Renomeie o diretório `PalDefender` em <span class="path">../Pal/Binaries/Win64/</span> e reinicie o servidor.</li>
  <li>Em certos casos, a instalação de <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ redistribuível</a> pode ajudar.</li>
</ul>

</details>


<details><summary style="font-size:16px">Não consigo ver certos símbolos corretamente no console do meu servidor.</summary>

<p>
Use o terminal Windows (ou qualquer alternativa com suporte unicode adequado) em vez do console windows padrão.
</p>

</details>



<details><summary style="font-size:16px">Como posso relatar falhas?</summary>

<p>
Envie os seguintes arquivos na <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">seção de problemas</a>:
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span>
</ul>
</p>

<p>
Certifique-se de descartar qualquer informação que você possa ver ou presumir que possa ser o motivo. Não se esqueça da versão PalDefender! Qualquer informação pode ser valiosa!
</p>

</details>

