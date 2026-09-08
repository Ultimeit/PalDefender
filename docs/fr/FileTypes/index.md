# 📁Types de fichiers

**PalDefender** prend en charge une gamme de types de fichiers personnalisés qui peuvent être utilisés pour configurer le comportement de votre serveur et étendre ses fonctionnalités.
Actuellement pris en charge :
* `Config.json`
* `WhiteList.json`
* `Banlist.json`
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json`
* `RESTAPI/RESTConfig.json`
* `RESTAPI/Tokens/*.json`

---

## ⚡ Aperçu rapide

### 🛠️ [Config.json](./Config.md)

Contrôle le comportement du serveur, la modération, la journalisation et les paramètres d'administration.

* **Sécurité :** Anti-triche (avertissement, kick, ban, IP-ban), filtrage name/word, protection SteamID, contrôles illégaux stat/item.
* **Journalisation :** Suit les discussions, RCON, les connexions, les décès, les convocations, l'activité de construction, les événements de plate-forme pétrolière.
* **Administrateur :** Liste blanche IP, connexion automatique, godmode/cheats, visibilité des actions de l'administrateur.
* **Annonces :** MOTD, décès de joueurs, invocations, punitions et événements de butin.
* **Limites de chat et de jeu :** Longueur du message, contournement du temps de recharge, plafonds de dégâts PvP/PvE, limite de coupe d'arbres.
* **Divers :** Prise en charge de RCON base64, gestion des échecs de démarrage, mode de commande chinois en option.

---

### 👥 `WhiteList.json`

Définit qui est autorisé à rejoindre le serveur.
Prend en charge les **ID utilisateur** et les **adresses IP** (y compris les plages masquées).

---

### 🚫 `Banlist.json`

Stocke les enregistrements d'interdiction PalDefender utilisés par les outils d'interdiction, de levée d'interdiction, d'interdiction IP et de punition REST.

* Préférez `/ban`, `/unban`, `/banip`, `/unbanip` ou le REST API au lieu de modifier ce fichier manuellement.
* Si vous devez le modifier manuellement, arrêtez d'abord le serveur ou rechargez la configuration après les modifications.

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Utilisé pour générer ou donner des Pals personnalisés via des commandes.

* Définit l'**ID, le surnom, le sexe, les statistiques (HP/SP/MP) du Pal, la faim, la santé mentale, le statut brillant, les compétences, les IV, les passifs**, et plus encore.
* Permet une personnalisation complète des **traits de combat, d'utilité et de travail** d'un Pal.

---

### 📍 [PalSummon.json](./PalSummon.md)

Génère un Pal personnalisé à un emplacement spécifique.

* Fait référence à un `PalTemplate`, définit la **position mondiale (X, Y, Z)**.
* Configure les indicateurs tels que **incapturable** et désactive des **effets de statut** spécifiques (par exemple, poison, noyade, brûlure, etc.).

---

### 🧾 [Pals/ImportRules/*.json](./PalImportRules.md)

Contrôle la façon dont les modèles Pal personnalisés sont acceptés.

* Définissez des limites globales dans `Pals/ImportRules/Default.json`.
* Ajoutez des remplacements per-Pal avec des fichiers tels que `Pals/ImportRules/Anubis.json`.
* Choisissez si les valeurs dépassées sont bloquées ou bridées.
* Choisissez si les passifs non autorisés bloquent les importations ou sont supprimés.

---

### 🌐 REST API fichiers de configuration

La configuration REST API réside dans `RESTAPI/RESTConfig.json`, tandis que les jetons du porteur résident dans `RESTAPI/Tokens/*.json`.

* `RESTConfig.json` contrôle si le API est activé, l'adresse de liaison, le port, la journalisation de la console et les paramètres CORS.
* Chaque fichier de jeton doit contenir un jeton privé et des autorisations. Ne partagez pas publiquement les valeurs des jetons.
