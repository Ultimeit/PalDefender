# FAQ

<details><summary style="font-size:16px">J'ai accidentellement banni myself/someone. Comment puis-je les annuler ?</summary>

<p style="font-size:14px">
Utilisez <span class="var-command">/unban &lt;UserId&gt;</span> pour les interdictions de compte et <span class="var-command">/unbanip &lt;IP&gt;</span> pour les interdictions IP. Les enregistrements d'interdiction PalDefender sont stockés dans <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>. Si vous modifiez le fichier manuellement, arrêtez d'abord le serveur ou rechargez la configuration après la modification.
</p>

</details>


<details><summary style="font-size:16px"><span class='pd-badge pd-badge--deprecated'>Deprecated</span> Ancien nettoyage d'interdiction IP via Config.json</summary>

<p style="font-size:14px">
Les anciennes versions du wiki demandaient aux administrateurs de supprimer les interdictions IP de <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span>. Ce chemin est obsolète pour les enregistrements d'interdiction. Utilisez <span class="var-command">/unbanip &lt;IP&gt;</span> ou modifiez plutôt <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Banlist.json</span>.
</p>

</details>


<details><summary style="font-size:16px">J'ai ajouté ou modifié un fichier PalTemplate ou PalSummon mais la commande échoue.</summary>

<ul>
  <li>Assurez-vous que le fichier est valide JSON. Supprimez les commentaires et les virgules finales.</li>
  <li>Les modèles appartiennent à <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Templates/</span>.</li>
  <li>Les invocations appartiennent à <span class="path-partial">../Pal/Binaries/Win64/PalDefender/Pals/Summons/</span>.</li>
  <li>Utilisez le nom de fichier sans chemin, par exemple <span class="var-command">/summon ArenaBoss</span>.</li>
  <li>Pour les fichiers d'invocation, vérifiez que <code>PalTemplate</code>, <code>X</code>, <code>Y</code> et <code>Z</code> sont présents.</li>
  <li>Pour les fichiers modèles, vérifiez que <code>PalID</code> est présent et utilise un ID Pal valide.</li>
</ul>

</details>


<details><summary style="font-size:16px">Quel identifiant dois-je utiliser pour les commandes : UserId, PlayerUId, name ou SteamID ?</summary>

<p>
La plupart des commandes d'administration attendent l'ID utilisateur du joueur, tel que <code>steam_...</code> ou <code>gdk_...</code>. Utilisez <span class="var-command">/iwantplayerlist</span> dans le jeu pour afficher les identifiants dans la liste des joueurs, ou utilisez l'outil REST/API si vous l'avez activé.
</p>

</details>


<details><summary style="font-size:16px">Pourquoi RCON nécessite-t-il des coordonnées ou un ID utilisateur pour les commandes qui fonctionnent sans elles dans le chat ?</summary>

<p>
RCON n'a pas de personnage de joueur dans le jeu, donc PalDefender ne peut pas déduire votre position ou votre cible. Pour les commandes telles que <span class="var-command">/getpos</span>, <span class="var-command">/tp</span>, <span class="var-command">/spawnpal</span> et les commandes d'emplacement de base, fournissez explicitement le joueur ou les coordonnées cible.
</p>

</details>


<details><summary style="font-size:16px">Le REST API renvoie 401 ou 403. Que dois-je vérifier ?</summary>

<ul>
  <li><strong>401</strong> : vérifiez l'en-tête <code>Authorization: Bearer &lt;token&gt;</code> et assurez-vous que le fichier de jeton ne s'appelle pas <code>TokenExample.json</code>.</li>
  <li><strong>403</strong> : vérifiez les autorisations du jeton et assurez-vous que le serveur a fini de démarrer.</li>
  <li>Après avoir modifié les jetons, redémarrez le serveur ou rechargez la configuration API/token en fonction de votre flux de travail hôte.</li>
</ul>

</details>



<details><summary style="font-size:16px">Je ne parviens pas à me connecter en tant qu'administrateur, il est indiqué que les commandes d'administrateur sont protégées par une liste blanche.</summary>

<p>
Assurez-vous d'avoir ajouté votre adresse IP à <span class="path-partial">../Pal/Binaries/Win64/PalDefender/</span><span class="file-partial">Config.json</span> comme ceci :
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
Alternativement, vous pouvez définir <span class="config-value">useAdminWhitelist</span> sur <span class="var-bool">false</span> mais cela n'est pas recommandé, car les tricheurs sont connus pour avoir une sorte d'exploit pour obtenir le mot de passe administrateur.
</p>

</details>



<details><summary style="font-size:16px">Mon serveur plante au démarrage.</summary>
<ul>
  <li>Assurez-vous que PalDefender est le seul mod en cours d'exécution — supprimez tous les autres mods et vérifiez si le problème persiste.</li>
  <li>Vérifiez si PalDefender est sur la version la plus récente.</li>
  <li>Consultez notre <a href="https://discord.gg/paldefender" target="_blank">discord</a> pour toute annonce.</li>
  <li>Renommer le répertoire `PalDefender` dans <span class="path">../Pal/Binaries/Win64/</span> et redémarrer le serveur.</li>
  <li>Dans certains cas, l'installation de <a href="https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170" target="_blank">VC++ redistribuable</a> peut aider.</li>
</ul>

</details>


<details><summary style="font-size:16px">Je ne vois pas correctement certains symboles dans la console de mon serveur.</summary>

<p>
Veuillez utiliser le terminal Windows (ou toute alternative avec une prise en charge Unicode appropriée) au lieu de la console windows par défaut.
</p>

</details>



<details><summary style="font-size:16px">Comment puis-je signaler des plantages ?</summary>

<p>
Envoyez les fichiers suivants dans la section <a href="https://github.com/Ultimeit/PalDefender/issues" target="_blank">issue</a> :
<ul>
  <li><span class="path-partial">.../Pal/Saved/Crashes/&lt;random numbers&gt;/</span><span class="file-partial">CrashContext.runtime-xml</span>
  <li><span class="path-partial">.../Pal/Binaries/Win64/PalDefender/Logs/</span><span class="file-partial">&lt;recent logs&gt;</span>
</ul>
</p>

<p>
Assurez-vous de supprimer toute information que vous pourriez voir ou supposer que cela pourrait en être la raison. N'oubliez pas la version PalDefender ! Toute information peut être précieuse !
</p>

</details>

