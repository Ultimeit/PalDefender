# Commandes

## Que sont les commandes ?

Les commandes sont des instructions textuelles spéciales qui vous permettent d'interagir avec le jeu. En tapant des commandes dans le chat, vous pouvez effectuer des actions telles que vous téléporter, faire apparaître des créatures ou gérer des joueurs. Les commandes commencent généralement par <span class="var-command">/</span> suivi du nom de la commande et des arguments facultatifs.

## Qui peut utiliser les commandes ?

**Actuellement, il n'existe aucune commande que les joueurs non-administrateurs peuvent utiliser.**
Dans la version actuelle, seules les commandes Admin et RCON sont disponibles.

## Liste des commandes

!!! note "Syntaxe des commandes"
    <span class="var-command">/command_name&nbsp;</span><span class="var-command-arg">&lt;required_argument&gt;&nbsp;</span><span class="var-command-optional">[optional_argument={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;required_argument&gt;</span> → Doit être inclus.<br>
    <span class="var-command-optional">[optional_argument={?}]</span> → Peut être omis. Le <span class="var-command-optional">{?}</span> indique la valeur par défaut utilisée en cas d'omission.
    </p>
    <p>
    Les arguments ont différents types. Les plus courants sont <span class="var-string">strings</span>, <span class="var-number">numbers</span>, <span class="var-float">floats</span> et <span class="var-bool">booleans</span>. Certaines commandes ont même des types complexes tels qu'un <span class="file">filenames</span> spécifique dans un répertoire spécial ou en fait un <span class="var-filter">filter</span>.
    </p>

!!! tip "Recherche d'identité"
    Utilisez [paldeck.cc/pals](https://paldeck.cc/pals) pour `PalID`, [paldeck.cc/items](https://paldeck.cc/items) pour `ItemID`, [paldeck.cc/technology](https://paldeck.cc/technology) pour `TechID`, [paldeck.cc/buildings](https://paldeck.cc/buildings) pour `BuildingID`, [paldeck.cc/passives](https://paldeck.cc/passives) pour `PassiveID` et [paldeck.cc/skills](https://paldeck.cc/skills) pour les identifiants de compétences.

??? note "RCON uniquement"
    ??? info "/getrconcmds"
        **Syntaxe :** `/getrconcmds`

        **Description :** Renvoie une liste de chaque commande avec le nombre d'arguments requis qui est utilisable par RCON.

        **Arguments :**

        - Aucun

        **Autorisations :** `RCON`

        **Exemple :**
        ```
        /getrconcmds
        ```

??? note "Gestion du serveur"
    ??? info "/version"
        **Syntaxe :** `/version`

        **Description :** Affiche la version du jeu Palworld et la version PalDefender. RCON renvoie la sortie JSON.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /version
        ```

    ??? info "/reloadcfg"
        **Syntaxe :** `/reloadcfg`

        **Description :** Recharge les données d'interdiction `Config.json`, `WhiteList.json` et PalDefender.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **Syntaxe :** `/addadminip <IP>`

        **Description :** Ajoute une adresse IP à la liste blanche des administrateurs.

        **Arguments :**

        - `<IP>` : L'adresse IP à ajouter en tant qu'administrateur.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **Syntaxe :** `/setadmin <UserId>`

        **Description :** Administrateur grants/revokes temporairement d'un joueur.

        **Arguments :**

        - `<UserId>` : ID du joueur pour l'administrateur grant/revoke.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **Syntaxe :** `/pgbroadcast <Message>`

        **Description :** Envoyez un message à tous les joueurs du serveur.

        **Arguments :**

        - `<Message>` : Le message à diffuser.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /pgbroadcast "Server will restart soon."
        ```

    ??? info "/adminlogin"
        **Syntaxe :** `/adminlogin <password>`

        **Description :** Vous connecte en mode administrateur. Nécessite votre mot de passe administrateur comme argument.

        **Arguments :**

        - `<password>` : le mot de passe administrateur.

        **Autorisations :** `Chat`

        **Exemple :**
        ```
        /adminlogin mySecretPassword
        ```

    ??? info "/adminlogout"
        **Syntaxe :** `/adminlogout`

        **Description :** Vous déconnecte du mode administrateur.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **Syntaxe :** `/iwantplayerlist`

        **Description :** Active la superposition de la liste des joueurs dans le jeu, vous permettant d'afficher l'ID utilisateur et l'UID du joueur lorsque vous appuyez sur ÉCHAP. Utile pour les administrateurs de serveur et les joueurs qui souhaitent voir des informations détaillées sur les joueurs directement dans l'interface du jeu.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **Syntaxe :** `/getpos [UserId]`

        **Description :** Obtient votre position actuelle dans le monde, qui peut être utilisée pour la téléportation, l'invocation et des actions similaires. Si un [UserId] est fourni, obtient à la place la position de ce joueur.

        **Arguments :**

        - `[UserId]` : (Facultatif) L'ID du joueur dont vous souhaitez obtenir la position. En cas d'omission, renvoie votre propre position.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **Syntaxe :** `/settime <hour>`

        **Description :** Modifie l'heure dans Palworld. L'heure peut avoir les valeurs suivantes : `0` à `23`, `day` et `night`.

        **Arguments :**

        - `<hour>` : Valeur horaire (0-23, jour, nuit).

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/togglepvp"
        **Syntaxe :** `/togglepvp`

        **Description :** Active ou désactive le serveur PvP pour la session en cours d'exécution.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /togglepvp
        ```

    ??? info "/alert"
        **Syntaxe :** `/alert <message>`

        **Description :** Envoie un message d'alerte à tous les joueurs du serveur. Ce message est généralement affiché bien en évidence sur leurs écrans.

        **Arguments :**

        - `<message>` : Le message à diffuser en alerte.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /alert Server will restart in 5 minutes!
        ```

    ??? info "/send"
        **Syntaxe :** `/send <type> <UserId> <Message>`

        **Description :** Vous permet d'envoyer un message ou un message de journal à un joueur spécifique.

        **Arguments :**

        - `<type>` : Le type de message à envoyer. Valeurs possibles :
             - `msg` : message de discussion régulier.
             - `log` : message de journal régulier (blanc, disparaît rapidement, police plus grande).
             - `ilog` : message de journal important (bleu, reste plus longtemps).
             - `vilog` : message de journal très important (bleu, reste extrêmement long).
        - `<UserId>` : L'ID du joueur qui recevra le message.
        - `<Message>` : Le texte du message à envoyer.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /send msg steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send log steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send ilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        /send vilog steam_76500000000000000 Dont miss out on Qonzer's sale!
        ```

    ??? info "/resetoilrig"
        **Syntaxe :** `/resetoilrig <lv30|lv55|lv60|all>`

        **Description :** Réinitialise la plate-forme pétrolière sélectionnée ou chaque plate-forme pétrolière actuellement gérée.

        **Autorisations :** `Chat`, statut d'administrateur actif dans le jeu.

        **Exemple :**
        ```
        /resetoilrig all
        ```

    ??? info "/setting"
        **Syntaxe :** `/setting list [filter]` ou `/setting <setting_name> <get|set|add|sub> [value]`

        **Description :** Inspecte ou modifie les valeurs `UPalGameSetting` en direct prises en charge. Les noms ne respectent pas la casse ; un préfixe ou une sous-chaîne unique est accepté. Ceci est expérimental, ne remplace pas la configuration mondiale persistante et les clients peuvent continuer à afficher les valeurs mises en cache.

        - `list [filter]` : répertorie les champs integer, float, booléens, octets et énumérations pris en charge.
        - `get` : Lit une valeur.
        - `set` : définit tout type pris en charge. Les booléens acceptent `true/false`, `on/off`, `yes/no` ou `1/0` ; les énumérations acceptent un numéro ou un nom d'entrée.
        - `add` / `sub` : modifie uniquement les valeurs numériques.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemples :**
        ```
        /setting list death
        /setting PalDeathPenaltyTime get
        /setting PalDeathPenaltyTime set 10
        ```

    ??? info "/resetbosstower"
        **Syntaxe :** `/resetbosstower <BossType|all>`

        **Description :** Commande de débogage uniquement qui réinitialise une instance de tour de boss ou toutes les tours de boss réinitialisables. Une seule cible doit utiliser un nom `EPalBossType` valide. Il n’est pas disponible dans les versions publiques.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /resetbosstower all
        ```

    ??? info "/showbosses"
        **Syntaxe :** `/showbosses`

        **Description :** Commande d'exploration de données de débogage uniquement qui écrit les informations statiques du boss actuel dans `PalDefender/Logs/BossInfo.json`. Il n’est pas disponible dans les versions publiques.

        **Autorisations :** `Chat`, `RCON`, `Admin`

??? note "Gestion des bases"
    ??? info "/findunusedbases (alias: /findbases)"
        **Syntaxe :** `/findbases [empty|inactive|unused|all] [days=N] [builds<=N]`

        **Syntaxe interactive :** `/findbases visit [filters]`, `/findbases next`, `/findbases kill [next]`

        **Description :** Recherche les bases vides, inactives ou inutilisées. `visit` crée une file d'attente de révision réservée au chat et se téléporte vers son premier résultat ; `next` avances ; `kill` détruit la base sélectionnée ; `kill next` le détruit et avance. La destruction est irréversible, alors inspectez d’abord chaque cible.

        - `empty` : Aucun ouvrier et au plus la limite de construction par défaut (ou `builds<=N`).
        - `inactive` : aucun membre de guilde en ligne et inactif depuis au moins `days` (par défaut `30`).
        - `unused` : correspond à des correspondances vides ou inactives.
        - `all` : répertorie toutes les bases tout en appliquant des filtres explicites.

        **Autorisations :** La liste prend en charge `Chat` et `RCON` ; visit/next/kill nécessite un chat en jeu et une autorisation d'administrateur.

        **Exemples :**
        ```
        /findbases empty builds<=5
        /findbases inactive days=14
        /findbases visit unused days=30
        /findbases kill next
        ```

    ??? info "/getnearestbase"
        **Syntaxe :** `/getnearestbase [X] [Y] [Z]`

        **Description :** Vous indique le nom de la guilde qui possède la base la plus proche de votre personnage.

        **Remarque :** Lorsqu'ils sont exécutés via **RCON**, tous les paramètres de localisation (`[X]` `[Y]` `[Z]`) **sont requis**, car RCON n'a aucun personnage de joueur pour déterminer l'emplacement.

        **Arguments :**

        - `[X]` : (Facultatif) Coordonnée X.
        - `[Y]` : (Facultatif) Coordonnée Y.
        - `[Z]` : (Facultatif) Coordonnée Z.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **Syntaxe :** `/gotonearestbase [X] [Y] [Z]`

        **Description :** Vous téléporte à la base la plus proche de l'emplacement.

        **Remarque :** Lorsqu'ils sont exécutés via **RCON**, tous les paramètres de localisation (`[X]` `[Y]` `[Z]`) **sont requis**, car RCON n'a aucun personnage de joueur pour déterminer l'emplacement.

        **Arguments :**

        - `[X]` : (Facultatif) Coordonnée X.
        - `[Y]` : (Facultatif) Coordonnée Y.
        - `[Z]` : (Facultatif) Coordonnée Z.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **Syntaxe :** `/killnearestbase [X] [Y] [Z]`

        **Description :** Détruit la base la plus proche (**À utiliser avec prudence !**).

        **Remarque :** Lorsqu'ils sont exécutés via **RCON**, tous les paramètres de localisation (`[X]` `[Y]` `[Z]`) **sont requis**, car RCON n'a aucun personnage de joueur pour déterminer l'emplacement.

        **Arguments :**

        - `[X]` : (Facultatif) Coordonnée X.
        - `[Y]` : (Facultatif) Coordonnée Y.
        - `[Z]` : (Facultatif) Coordonnée Z.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /killnearestbase 100 200 50
        ```


??? note "Gestion des joueurs"
    ??? info "/kick"
        **Syntaxe :** `/kick <UserId> [Reason="Kicked by Admin."]`

        **Description :** Expulse un joueur du serveur.

        **Arguments :**

        - `<UserId>` : ID du joueur à expulser.
        - `[Reason]` : (Facultatif) Raison du coup de pied. Par défaut : "Expulsé par l'administrateur".

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /kick steam_76500000000000000 "Spamming in chat"
        ```

    ??? info "/ban"
        **Syntaxe :** `/ban <UserId> [Reason="Banned by Admin."]`

        **Description :** Bannit et expulse un joueur du serveur.

        **Arguments :**

        - `<UserId>` : L'ID du joueur à bannir.
        - `[Reason]` : (Facultatif) Raison de l'interdiction. Par défaut : "Banni par l'administrateur".

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /ban gdk_25300000000000000 "Cheating"
        ```

    ??? info "/ipban"
        **Syntaxe :** `/ipban <UserId> [Reason="Banned by Admin."]`

        **Description :** Bannit l'adresse IP d'un joueur, puis l'expulse du serveur.

        **Arguments :**

        - `<UserId>` : L'ID du joueur à bannir IP.
        - `[Reason]` : (Facultatif) Raison de l'interdiction. Par défaut : "Banni par l'administrateur".

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **Syntaxe :** `/banip <IP>`

        **Description :** Interdit une adresse IP du serveur.

        **Arguments :**

        - `<IP>` : L'adresse IP à interdire.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **Syntaxe :** `/unbanip <IP>`

        **Description :** Supprime une adresse IP de la liste de bannissement.

        **Arguments :**

        - `<IP>` : l'adresse IP à débloquer.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/unban"
        **Syntaxe :** `/unban <UserId> [Reason="Unbanned by admin."]`

        **Description :** Supprime un ID utilisateur de la liste d'interdiction PalDefender.

        **Arguments :**

        - `<UserId>` : l'ID utilisateur à débloquer.
        - `[Reason]` : (Facultatif) Raison stockée pour l'action d'annulation du bannissement.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /unban steam_76500000000000000 "Appeal accepted"
        ```

    ??? info "/getip"
        **Syntaxe :** `/getip <UserId>`

        **Description :** Vous montre l'adresse IP d'un joueur.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **Syntaxe :** `/whitelist_add <UserId>`

        **Description :** Ajoute un UserId à la liste blanche.

        **Arguments :**

        - `<UserId>` : l'ID du joueur à ajouter à la liste blanche.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **Syntaxe :** `/whitelist_remove <UserId>`

        **Description :** Supprime un ID utilisateur de la liste blanche.

        **Arguments :**

        - `<UserId>` : L'ID du joueur à supprimer de la liste blanche.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **Syntaxe :** `/whitelist_get`

        **Description :** Affiche la liste complète des joueurs sur la liste blanche.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **Syntaxe :** `/imcheater`

        **Description :** Utilisez ceci pour tester la façon dont votre serveur répond à un tricheur.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **Syntaxe :** `/spectate`

        **Description :** Active le mode spectateur. Identique à appuyer sur la touche de raccourci `\`, mais la touche de raccourci ne fonctionne pas pour tout le monde, comme pour les joueurs sur console.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /spectate
        ```

??? note "Personnage du joueur"
    ??? info "/tp"
        **Syntaxe :**
        L'une des œuvres suivantes :

        - `/tp <UserId>`
        - `/tp <UserId1> <UserId2>`
        - `/tp <X> <Y>`
        - `/tp <X> <Y> <Z>`
        - `/tp <UserId> <X> <Y>`
        - `/tp <UserId> <X> <Y> <Z>`
        - `/tp home`
        - `/tp oilrig`
        - `/tp oilrig:Lv30`
        - `/tp oilrig:Lv55`
        - `/tp oilrig:Lv60`

        **Description :** Vous téléporte, ou téléporte un joueur spécifié, vers un autre joueur, ses coordonnées, la base possédée la plus proche ou une destination de plate-forme pétrolière.

        **Remarque :** RCON doit inclure le joueur téléporté car RCON n'a pas de personnage dans le jeu.

        **Arguments :**

        - `<UserId>` : Un joueur vers lequel se téléporter, ou le joueur téléporté lorsque plus d'arguments sont fournis.
        - `<UserId1>` : Le joueur à téléporter.
        - `<UserId2>` : Le joueur cible.
        - `<X> <Y> [Z]` : Coordonnées de la carte. Si `Z` est omis, PalDefender essaie de trouver une hauteur de sol utilisable.
        - `home` : se téléporte vers la base possédée la plus proche.
        - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60` : se téléporte vers une destination de plate-forme pétrolière.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        /tp 100 -250
        /tp oilrig:Lv60
        ```

    ??? info "/give_exp"
        **Syntaxe :** `/give_exp <UserId> <Amount>`

        **Description :** Donne des points d'expérience à un joueur.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<Amount>` : Nombre de points d'expérience.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **Syntaxe :** `/giveme_exp <Amount>`

        **Description :** Vous donne des points d'expérience.

        **Arguments :**

        - `<Amount>` : Nombre de points d'expérience.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **Syntaxe :** `/renameplayer <UserId> <NewName>`

        **Description :** Renomme le surnom d'un joueur.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<NewName>` : Le nouveau pseudo.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /renameplayer steam_76500000000000000 NewNickname
        ```

    ??? info "/givestats"
        **Syntaxe :** `/givestats <UserId> [Count=1]`

        **Description :** Donne au joueur un ou plusieurs points de statut inutilisés (une valeur négative sera soustraite). N'affecte pas les points déjà dépensés.

        **Arguments :**

        - `<UserId>` : L'ID du joueur qui recevra les points de statut.
        - `[Count]` : (Facultatif) Le nombre de points de statut inutilisés à donner (peut être négatif à soustraire). Par défaut : 1.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **Syntaxe :** `/givemestats [Count=1]`

        **Description :** Vous donne un ou plusieurs points de statut inutilisés (une valeur négative sera soustraite). N'affecte pas les points déjà dépensés.

        **Arguments :**

        - `[Count]` : (Facultatif) Le nombre de points de statut inutilisés à vous accorder (peut être négatif à soustraire). Par défaut : 1.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **Syntaxe :** `/godmode [on/off]`

        **Description :** Accorde l'invulnérabilité, y compris l'immunité aux effets de statut, refuse la consommation de nourriture et restaure la santé lors de l'activation. Permet éventuellement de tout filmer en une seule fois, si activé dans la configuration.

        **Arguments :**

        - `[on/off]` : (Facultatif) Pour activer ou désactiver explicitement le godmode. Par défaut : active et désactive.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

    ??? info "/admingun (alias: /agun)"
        **Syntaxe :** `/admingun`

        **Description :** Donne à un administrateur actif dans le jeu une Admin Gun protégée. Elle tue instantanément les personnages, détruit les objets de la carte, maximise les dégâts infligés au feuillage, possède des munitions et une durabilité illimitées et ne peut pas être jetée, vendue ou déplacée vers des conteneurs externes. Accroupissez-vous lors de la destruction d'un objet de stockage pour supprimer son contenu ; restez debout pour le conserver. L'arme est retirée à la mort, à la déconnexion ou lors de la perte du statut d'administrateur. En demander une autre remplace l'exemplaire existant.

        **Autorisations :** `Chat`, statut d'administrateur actif dans le jeu. `allowAdminCheats` n’est pas requis.

        **Exemple :**
        ```
        /agun
        ```

??? note "Gestion de guilde"
    ??? info "/setguildleader"
        **Syntaxe :** `/setguildleader <UserId>`

        **Description :** Fait du joueur ciblé le chef de sa guilde actuelle.

        **Arguments :**

        - `<UserId>` : L'ID du joueur à devenir chef de guilde.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **Syntaxe :** `/exportguilds`

        **Description :** Déverse chaque guilde du serveur dans Pal/Binaries/Win64/PalDefender/guildexport.json.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /exportguilds
        ```
        Exemple de fichier de sortie : `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "Articles"
    ??? info "/give"
        **Syntaxe :** `/give <UserId> <ItemId> [Amount=1]`

        **Description :** Donne au joueur un objet et, si spécifié, combien.

        **Arguments :**

        - `<UserId>` : l'ID du joueur à qui donner l'objet.
        - `<ItemId>` : l'objet à donner.
        - `[Amount]` : (Facultatif) Combien. Par défaut : 1.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **Syntaxe :** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **Description :** Donne à un joueur plus d'un élément dans une seule commande et, si spécifié, combien de chaque élément est séparé par deux points.

        **Arguments :**

        - `<UserId>` : l'ID du joueur à qui donner les objets.
        - `<ItemId>[:<Amount>] ...` : Liste des postes et montants optionnels.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **Syntaxe :** `/giveme <ItemId> [Amount=1]`

        **Description :** Vous donne un article et, si précisé, combien.

        **Arguments :**

        - `<ItemId>` : L'objet à s'offrir.
        - `[Amount]` : (Facultatif) Combien. Par défaut : 1.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **Syntaxe :** `/delitem <UserId> <ItemId> [Amount=1]`

        **Description :** Supprime d'un joueur la quantité indiquée d'un objet. La valeur par défaut est `1`, ce qui ne supprime qu'une occurrence. Utilisez `all` au lieu de `1` pour supprimer toutes les occurrences.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<ItemId>` : L'objet à supprimer.
        - `[Amount]` : (Facultatif) Quantité. Par défaut : 1. Utilisez `all` pour supprimer toutes les occurrences.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **Syntaxe :** `/give_relic <UserId> <RelicType> [Amount]`

        **Description :** Donne au joueur un ou plusieurs points de relique du type sélectionné.

        **Arguments :**

        - `<UserId>` : L'ID du joueur qui recevra les points de relique.
        - `<RelicType>` : Le type de relique à accorder.

        - `[Amount]` : Nombre optionnel de points de relique à donner. La valeur par défaut est `1`.

        **Types de reliques pris en charge :** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /give_relic steam_76500000000000000 CapturePower 5
        ```

    ??? info "/giveme_relic"
        **Syntaxe :** `/giveme_relic <RelicType> [Amount]`

        **Description :** Vous donne un ou plusieurs points de relique du type sélectionné.

        **Arguments :**

        - `<RelicType>` : Le type de relique à accorder.

        - `[Amount]` : Nombre optionnel de points de relique à s'offrir. La valeur par défaut est `1`.

        **Types de reliques pris en charge :** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /giveme_relic CapturePower 5
        ```


    ??? info "/delitems"
        **Syntaxe :** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **Description :** Supprime plusieurs objets d'un joueur en une seule commande. La quantité facultative de chaque objet est séparée par deux-points. Utilisez `all` au lieu de `1` pour supprimer toutes les occurrences.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<ItemId>[:<Amount>] ...` : Liste des postes et montants optionnels.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **Syntaxe :** `/clearinv <UserId> [Container=items] ...`

        **Description :** Supprime les conteneurs spécifiés de l'inventaire d'un joueur. Conteneurs disponibles : `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot` ou `all`.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `[Container] ...` : (Facultatif) Conteneurs à effacer. Par défaut : éléments.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "Pals"
    ??? info "/givepal"
        **Syntaxe :** `/givepal <UserId> <PalId> [Level=1]`

        **Description :** Donne un Pal à un joueur du niveau spécifié.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<PalId>` : Le Pal à donner.
            - **Remarque :** Utilisez l'ID Pal, par exemple, `WeaselDragon` (Chillet). Voir la liste complète sur [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]` : (Facultatif) Niveau du Pal. Par défaut : 1.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **Syntaxe :** `/givepal_j <UserID> <PalTemplate>`

        **Description :** Donne à un joueur un Pal défini par un fichier PalTemplate. JSON intégré n'est plus pris en charge ; seul un nom de fichier est accepté.

        **Remarque :** Vous n'avez pas besoin d'inclure l'extension .json dans le nom de fichier ; le système l'ajoutera automatiquement s'il est manquant.

        **Arguments :**

        - `<UserID>` : l'identifiant du joueur.
        - `<PalTemplate>` : Le nom du fichier PalTemplate (voir [PalTemplate](../FileTypes/PalTemplate.md)).

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **Syntaxe :** `/givemepal <PalId> [Level=1]`

        **Description :** Vous donne un Pal au niveau spécifié.

        **Arguments :**

        - `<PalId>` : Le Pal à se donner.
            - **Remarque :** Utilisez l'ID Pal, par exemple, `WeaselDragon` (Chillet). Voir la liste complète sur [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]` : (Facultatif) Niveau du Pal. Par défaut : 1.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **Syntaxe :** `/givemepal_j <PalTemplate>`

        **Description :** Vous donne un Pal défini par un fichier PalTemplate. JSON intégré n'est plus pris en charge ; seul un nom de fichier est accepté.

        **Arguments :**

        - `<PalTemplate>` : Le nom du fichier PalTemplate (voir [PalTemplate](../FileTypes/PalTemplate.md)).

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **Syntaxe :**
        L'une des œuvres suivantes :

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **Description :** Génère un Pal relatif ou absolu par rapport à vous. **RCON doit spécifier x, y et z !**

        **Remarque :** Toutes les statistiques, à l'exception du niveau, sont aléatoires.

        **Arguments :**
        - `<PalID>` : Le Pal à apparaître.
        - `[x]` : (Facultatif) x position du pal. Par défaut : relatif au joueur-invocateur.
        - `[y]` : (Facultatif) position du pal. Par défaut : relatif au joueur-invocateur.
        - `[z]` : (Facultatif) position z du pal. Par défaut : relatif au joueur-invocateur.
        - `[Level]` : (Facultatif) Niveau du Pal. Par défaut : 1.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /spawnpal Anubis 255
        ```
        _Fait naître un Anubis de niveau 255 !_

    ??? info "/spawnpal_ex"
        **Syntaxe :** Identique à `/spawnpal`.

        **Description :** Génère un Pal exactement comme `/spawnpal`, mais permet le suivi des dégâts. Lorsque le Pal meurt ou est capturé, PalDefender enregistre le classement complet des dégâts et l'envoie à `PalWebhooks.webhookURL_Summons` lorsque ce webhook est configuré. Si `announceAdminSummonsKill` est activé, les joueurs en ligne participants reçoivent également une boîte de dialogue de résultats affichant les cinq premiers et leur propre classement. Le donneur de dégâts le plus élevé est désigné comme gagnant. Cette commande n'utilise pas de fichier PalTemplate ou PalSummon et n'accorde pas de récompenses.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /spawnpal_ex Anubis 230 -486 4097 80
        ```

    ??? info "/spawnnpc"
        **Syntaxe :** `/spawnnpc <NPCID|CharacterID> [Level=1]` ou `/spawnnpc <NPCID|CharacterID> <X> <Y> [Z] [Level=1]`

        **Description :** Génère un NPC avec l'IA. Dans le chat, les coordonnées omises apparaissent près de l'administrateur ; RCON doit fournir les coordonnées. Avec seulement `X` et `Y`, PalDefender trouve la hauteur du sol.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /spawnnpc PIDF_Soldier_AssaultRifle 30
        ```

    ??? info "/spawnpal_j"
        **Syntaxe :**

        L'une des œuvres suivantes :

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal_j <PalTemplate> [x] [y] [z]`

        **Description :** Génère un Pal relatif ou absolu par rapport à vous. **RCON doit spécifier x, y et z !**

        **Remarque :** Toutes les statistiques, à l'exception du niveau, sont aléatoires.

        **Arguments :**

        - `<PalTemplate>` : Le nom du fichier PalTemplate à utiliser.
        - `[x]` : (Facultatif) x position du pal. Par défaut : relatif au joueur-invocateur.
        - `[y]` : (Facultatif) position du pal. Par défaut : relatif au joueur-invocateur.
        - `[z]` : (Facultatif) position z du pal. Par défaut : relatif au joueur-invocateur.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /spawnpal_j ArenaBoss 230 -486 4097
        ```

    ??? info "/spawnpal_ex_j"
        **Syntaxe :** `/spawnpal_ex_j <PalTemplate> [x] [y] [z]`

        **Description :** Utilise le même PalTemplate et la même gestion des coordonnées que `/spawnpal_j`, mais permet le suivi des dommages. Lorsque le Pal meurt ou est capturé, PalDefender enregistre le classement complet des dégâts et l'envoie à `PalWebhooks.webhookURL_Summons` lorsque ce webhook est configuré. Si `announceAdminSummonsKill` est activé, les joueurs en ligne participants reçoivent également une boîte de dialogue de résultats affichant les cinq premiers et leur propre classement. Le donneur de dégâts le plus élevé est désigné comme gagnant. Cette commande n'utilise pas les récompenses PalSummon.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /spawnpal_ex_j ArenaBoss 230 -486 4097
        ```

    ??? info "/summon"
        **Syntaxe :** `/summon <PalSummon>`

        **Description :** Génère un Pal à l'aide du fichier PalSummon fourni.

        **Remarque :** Vous n'avez pas besoin d'inclure l'extension .json dans le nom de fichier ; le système l'ajoutera automatiquement s'il est manquant.

        **Arguments :**
        - `<PalSummon>` : Le nom du fichier PalSummon à utiliser.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **Syntaxe :** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **Description :** Donne à l'utilisateur cible un œuf pal avec le pal spécifique à l'intérieur et un niveau éventuellement ajusté.

        **Arguments :**

        ??? quote "<UserId\>"
            **Description :** L'identifiant du joueur qui recevra l'œuf.

        ??? quote "<EggId\>"
            **Description :** Le type d'œuf à donner.

            **Remarque :** Les valeurs autorisées vont de 01 (la plus petite) à 05 (la plus grande) pour chaque type :

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **Description :** Le Pal qui sera à l'intérieur de l'œuf.

            **Remarque :** Utilisez l'ID Pal, par exemple, `WeaselDragon` (Chillet). Voir la liste complète sur [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Niveau\]"
            **Description :** (Facultatif) Le niveau du Pal à l'intérieur de l'œuf.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **Syntaxe :** `/givemeegg <EggId> <PalId> [Level]`

        **Description :** Offrez-vous un œuf pal avec le pal spécifique à l'intérieur et un niveau éventuellement ajusté.

        **Arguments :**

        ??? quote "<EggId\>"
            **Description :** Le type d'œuf à s'offrir.

            **Remarque :** Les valeurs autorisées vont de 01 (la plus petite) à 05 (la plus grande) pour chaque type :

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalId\>"
            **Description :** Le Pal qui sera à l'intérieur de l'œuf.

            **Remarque :** Utilisez l'ID Pal, par exemple, `WeaselDragon` (Chillet). Voir la liste complète sur [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Niveau]"
            **Description :** (Facultatif) Le niveau du Pal à l'intérieur de l'œuf.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **Syntaxe :** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **Description :** Donne un œuf pal avec un Pal défini par un fichier PalTemplate et un niveau éventuellement ajusté.

        **Arguments :**

        ??? quote "<EggId\>"
            **Description :** Le type d'œuf à donner.

            **Remarque :** Les valeurs autorisées vont de 01 (la plus petite) à 05 (la plus grande) pour chaque type :

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **Description :** Le nom du fichier PalTemplate à utiliser.

            **Remarque :** Vous n'avez pas besoin d'inclure l'extension .json dans le nom de fichier ; le système l'ajoutera automatiquement s'il est manquant. Voir [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Niveau]"
            **Description :** (Facultatif) Le niveau du Pal à l'intérieur de l'œuf.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **Syntaxe :** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **Description :** Offrez-vous un œuf pal avec un Pal défini par un fichier PalTemplate et un niveau éventuellement ajusté.

        **Arguments :**

        ??? quote "<EggI\>"
            **Description :** Le type d'œuf à s'offrir.

            **Remarque :** Les valeurs autorisées vont de 01 (la plus petite) à 05 (la plus grande) pour chaque type :

            - `PalEgg_Dark_01`–`PalEgg_Dark_05`
            - `PalEgg_Dragon_01`–`PalEgg_Dragon_05`
            - `PalEgg_Earth_01`–`PalEgg_Earth_05`
            - `PalEgg_Electricity_01`–`PalEgg_Electricity_05`
            - `PalEgg_Fire_01`–`PalEgg_Fire_05`
            - `PalEgg_Ice_01`–`PalEgg_Ice_05`
            - `PalEgg_Leaf_01`–`PalEgg_Leaf_05`
            - `PalEgg_Normal_01`–`PalEgg_Normal_05`
            - `PalEgg_Water_01`–`PalEgg_Water_05`

        ??? quote "<PalTemplate\>"
            **Description :** Le nom du fichier PalTemplate à utiliser.

            **Remarque :** Vous n'avez pas besoin d'inclure l'extension .json dans le nom de fichier ; le système l'ajoutera automatiquement s'il est manquant. Voir [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Niveau]"
            **Description :** (Facultatif) Le niveau du Pal à l'intérieur de l'œuf.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **Syntaxe :** `/jetragon`

        **Description :** Vous donne un Admin-Jetragon Pal (c'est faaas... parti).

        **Arguments :**
        - Aucun

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **Syntaxe :** `/catwaifu`

        **Description :** Vous donne un Admin-Cat-Waifu qui améliore les statistiques de votre personnage.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **Syntaxe :** `/exportpals [UserId]`

        **Description :** Exportez chaque Pal d'un lecteur vers un fichier PalTemplate dans Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/.

        **Arguments :**

        - `[UserId]` : (Facultatif) L'ID du joueur dont Pals sera exporté. En cas d'omission, exporte votre propre Pals.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **Syntaxe :** `/deletepals <UserId> <PalFilter>`

        **Description :** Supprime Pals de l'utilisateur spécifié à l'aide de filtres avancés. Le filtre vous permet de spécifier plusieurs critères (tels que Pal ID, niveau, sexe, passifs, etc.) en une seule commande. Veuillez tester dans un environnement sûr avant de l'utiliser sur des données importantes.

        **Arguments :**

        ??? quote "<UserId\>"
            **Description :** L'ID du joueur dont Pals sera supprimé.

        ??? quote "<PalFilter\>"
            **Description :** Un ensemble de mots-clés de filtrage permettant de sélectionner les Pals à supprimer.

            **Remarque :** Plusieurs mots-clés peuvent être combinés en une seule commande.

            Mots-clés de filtre disponibles :

            - `ID` : PalID ou liste de PalID (séparés par des virgules)
            - `Nick` : String (nom du Pal)
            - `Gender` : `male` ou `female`
            - `Level` : Nombre, prend en charge les symboles `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank` : Nombre, prend en charge les symboles `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky` : `true` ou `false` (brillant)
            - `Passives` : PassiveSkill ou liste de PassiveSkills (séparées par des virgules)
            - `Limit` : Nombre (nombre maximal de Pals à supprimer)

            **Exemples de filtres :**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            Les clés de filtre et les exemples ci-dessus sont la référence actuelle de PalFilter.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "Arbre de recherche"
    ??? info "/learntech"
        **Syntaxe :** `/learntech <UserId> <TechID>`

        **Description :** Permet à un joueur d'apprendre une technologie spécifique. Utilisez `all` pour tout déverrouiller.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<TechID>` : La technologie pour apprendre. Utilisez `all` pour tout débloquer.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **Syntaxe :** `/unlearntech <UserId> <TechID>`

        **Description :** Fait oublier au joueur une technologie spécifique. Utilisez `all` pour tout supprimer.

        **Arguments :**

        - `<UserId>` : l'identifiant du joueur.
        - `<TechID>` : La technologie à oublier. Utilisez `all` pour tout supprimer.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **Syntaxe :** `/givetechpoints <UserId> [Amount=1]`

        **Description :** Donne à l'utilisateur cible X points technologiques.

        **Arguments :**

        - `<UserId>` : L'ID du joueur qui recevra les points technologiques.
        - `[Amount]` : (Facultatif) Le nombre de points technologiques à donner. Par défaut : 1.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **Syntaxe :** `/givebosstechpoints <UserId> [Amount=1]`

        **Description :** Donne à l'utilisateur cible X points de technologie ancienne.

        **Arguments :**

        - `<UserId>` : L'ID du joueur qui recevra les anciens points technologiques.
        - `[Amount]` : (Facultatif) Le nombre de points de technologie ancienne à donner. Par défaut : 1.

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **Syntaxe :** `/givemetechpoints [Amount=1]`

        **Description :** Vous donne X points technologiques.

        **Arguments :**

        - `[Amount]` : (Facultatif) Le nombre de points technologiques à vous accorder. Par défaut : 1.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **Syntaxe :** `/givemebosstechpoints [Amount=1]`

        **Description :** Vous donne X points de technologie ancienne.

        **Arguments :**

        - `[Amount]` : (Facultatif) Le nombre de points de technologie ancienne à se donner. Par défaut : 1.

        **Autorisations :** `Chat`, `Admin`

        **Exemple :**
        ```
        /givemebosstechpoints 5
        ```


??? note "Exploration de données"
    ??? info "/gettechids"
        **Syntaxe :** `/gettechids`

        **Description :** Renvoie une liste de tous les ID de technologie disponibles. RCON obtient la sortie JSON.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **Syntaxe :** `/getskinids`

        **Description :** Renvoie une liste de tous les ID de skin Pal disponibles. RCON obtient la sortie JSON.

        **Arguments :**

        - Aucun

        **Autorisations :** `Chat`, `RCON`, `Admin`

        **Exemple :**
        ```
        /getskinids
        ```
