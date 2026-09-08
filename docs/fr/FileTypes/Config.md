# 🛠️ `Config.json`

`Config.json` est généré dans `<PalServer>/Pal/Binaries/Win64/PalDefender/` au premier démarrage. Arrêtez le serveur avant de le modifier ou utilisez `/reloadcfg` après avoir enregistré les modifications.

!!! note "Paramètres générés"
    PalDefender réécrit le paramètre actuel défini dans ce fichier. Les clés non répertoriées ci-dessous sont obsolètes, réservées à la migration ou indisponibles dans la version publique actuelle.

## Général et application

| Clé | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `version` | string | Version actuelle | Marqueur de configuration schema/version maintenu par PalDefender. |
| `MOTD` | array | Trois messages | Rejoignez les messages. Prend en charge `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}` et `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | bool | `true` | Arrête le serveur si PalDefender ne peut pas s'initialiser. Certains hôtes peuvent interpréter cela comme un crash et redémarrer à plusieurs reprises. |
| `preventAdminPasswordInChat` | bool | `true` | Empêche l'envoi du mot de passe administrateur sous forme de texte de discussion. |
| `shouldWarnCheaters` | bool | `true` | Avertit un joueur lorsqu'une détection automatique se déclenche. |
| `shouldWarnCheatersReason` | bool | `false` | Inclut la raison de la détection dans cet avertissement. |
| `shouldKickCheaters` | bool | `true` | Kicks a détecté les tricheurs à moins qu'une action activée plus forte ne s'applique. |
| `shouldBanCheaters` | bool | `false` | Les bannissements de compte ont détecté des tricheurs. |
| `shouldIPBanCheaters` | bool | `false` | Les interdictions IP ont détecté des tricheurs. |
| `blockEmergencyRespawn` | bool | `true` | Bloque l'action Menu → Réapparition d'urgence. |

## RCON et journalisation

| Clé | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` | Quelques secondes avant l'expiration d'une connexion RCON inactive. |
| `RCONbase64` | bool | `false` | Active les commandes RCON codées en base64. |
| `logNetworking` | bool | `false` | Écrit la journalisation réseau prise en charge. La journalisation réseau est désactivée dans la version publique actuelle. |
| `logNetworkingToConsole` | bool | `true` | Met en miroir la journalisation réseau sur la console lorsque la journalisation réseau est disponible. |
| `logChat` | bool | `true` | Enregistre les discussions globales, de guilde et de Say. |
| `logRCON` | bool | `false` | Enregistre les commandes RCON. |
| `logPlayerUID` | bool | `false` | Inclut PlayerUID dans les journaux pertinents et les webhooks anti-triche. |
| `logPlayerIP` | bool | `true` | Inclut les adresses IP dans les journaux pertinents et les webhooks anti-triche. |
| `logPlayerDeaths` | bool | `true` | Enregistre les morts et les meurtres de joueurs. |
| `logPlayerLogins` | bool | `true` | Enregistre les arrivées et départs des joueurs. |
| `logPlayerBuildings` | bool | `true` | Les journaux prennent en charge les activités de construction, d’annulation, de démantèlement et de déplacement de Palbox. |
| `logPlayerSummons` | bool | `true` | Enregistre les invocations de boss de raid des joueurs. |
| `logPlayerCaptures` | bool | `true` | Paramètre de compatibilité réservé. La journalisation des captures est désactivée dans la version 1.9.0 car l'événement disponible n'est pas fiable. |
| `logPlayerDamage` | bool | `false` | Enregistre les événements de dégâts provoqués par les joueurs et leurs valeurs de dégâts native/base signalées sur la console du serveur. Fonctionne indépendamment de la détection des tricheurs de dégâts. |
| `BannedCampWorker` | array | Variantes de Panthalus | ID de personnage qui ne peuvent pas être attribués dans une base. La correspondance n'est pas sensible à la casse ; les variantes telles que `BOSS_...` doivent être répertoriées séparément. |
| `logHelicopterKills` | bool | `true` | Enregistre les victimes d'hélicoptères de combat. |
| `logCraftings` | bool | `true` | Enregistre la création du joueur. |
| `logTechUnlocks` | bool | `true` | La technologie des journaux se déverrouille. |
| `logOpenOilrigBoxes` | bool | `true` | Enregistre les événements de la boîte de but de fin de plate-forme pétrolière. |
| `OilrigGoalBoxLocktime` | entier | `300` | Pendant quelques secondes, la boîte d'objectif de fin de plate-forme pétrolière reste verrouillée. |

## Webhooks Discord

`PalWebhooks` est un object. Laissez une URL individuelle vide pour désactiver cette destination. La livraison des webhooks est mise en file d'attente, de sorte que les rafales sont échelonnées au lieu de bloquer le fil de jeu.

| Clé imbriquée | Envoie |
| --- | --- |
| `webhookURL_Chat` | Messages de discussion globaux et dictés. |
| `webhookURL_GuildChat` | Messages de discussion de guilde avec le nom de la guilde. |
| `webhookURL_Commands` | Les commandes s'exécutent via le chat en jeu, y compris l'administrateur et la commande complète. |
| `webhookURL_Deaths` | Des morts et des meurtres. Nécessite `announcePlayerDeaths` ou `logPlayerDeaths`. |
| `webhookURL_JoinLeave` | Événements Join/leave lorsque `announceConnections` est activé ; respecte `dontAnnounceAdminConnections`. |
| `webhookURL_Summons` | Annonces d'invocation Player/admin et résultats complets des dégâts d'invocation suivis. |
| `webhookURL_Oilrig` | Les boîtes de plate-forme pétrolière et les hélicoptères tuent lorsque le paramètre `announce...` correspondant est activé. |
| `webhookURL_AntiCheats` | Détections anti-triche automatiques et manuelles. L'inclusion de UID/IP suit `logPlayerUID` et `logPlayerIP`. |

```json
"PalWebhooks": {
    "webhookURL_Chat": "",
    "webhookURL_GuildChat": "",
    "webhookURL_Commands": "",
    "webhookURL_Deaths": "",
    "webhookURL_JoinLeave": "",
    "webhookURL_Summons": "",
    "webhookURL_Oilrig": "",
    "webhookURL_AntiCheats": ""
}
```

## Administration, chat et annonces

| Clé | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` | Restreint l'administrateur login/commands à `adminIPs`. |
| `adminAutoLogin` | bool | `false` | Active automatiquement le mode administrateur pour rejoindre une adresse IP sur liste blanche. |
| `adminIPs` | array | `127.0.0.1` | Les adresses IP exactes et les entrées génériques prises en charge sont autorisées à administrer le serveur. |
| `bannedChatWords` | array | Termes RMT courants | Termes de filtre de discussion insensibles à la casse. |
| `bannedNames` | array | Noms d'abus connus | Noms de joueurs rejetés lors de la connexion. |
| `allowAdminCheats` | bool | `false` | Permet aux administrateurs d'utiliser les commandes dans `adminCheats` et de contourner les protections sélectionnées. L'Admin Gun lui-même ne nécessite que le statut d'administrateur actif dans le jeu. |
| `allowGodmodeOnehit` | bool | `false` | Permet aux utilisateurs de Godmode d'infliger des dégâts en un seul coup. |
| `adminCheats` | array | Liste générée | Commandes traitées comme des astuces d'administrateur lorsque `allowAdminCheats` est désactivé. RCON n'est pas bloqué par cette liste. |
| `announceConnections` | bool | `false` | Annonce joins/leaves dans le chat et active la source du webhook join/leave. |
| `dontAnnounceAdminConnections` | bool | `true` | Masque l’administrateur joins/leaves de ces annonces. |
| `announcePunishments` | bool | `false` | Annonce une triche automatique kicks/bans. |
| `announcePlayerDeaths` | bool | `false` | Annonce les décès de joueurs dans le chat. |
| `announceOpenOilrigBoxes` | bool | `false` | Annonce les événements de la boîte Oil Rig et active leur source de webhook. |
| `announceHelicopterKills` | bool | `false` | Annonce les victimes d'hélicoptères et active leur source de webhook. |
| `announcePlayerSummons` | bool | `false` | Annonce les invocations de boss de raid des joueurs. |
| `announceAdminSummons` | bool | `false` | Annonce Pals généré via les fonctionnalités d'invocation administrative. |
| `announceAdminSummonsKill` | bool | `true` | Annonce kills/deaths de Pals convoqué administrativement. |
| `chatBypassWait` | bool | `true` | Supprime l'attente normale de discussion entre les messages. |
| `chatMessageMaxLen` | entier | `128` | Longueur maximale acceptée des messages de discussion. |
| `useWhitelist` | bool | `false` | Active `WhiteList.json`. |
| `whitelistMessage` | string | Texte généré | Message affiché à un joueur rejeté qui ne figure pas sur la liste blanche. |
| `steamidProtection` | bool | `true` | Rejette l’utilisation simultanée en double d’un UserId. |

## Validation du gameplay

| Clé | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | entier | `100` | Dommages PvP maximum autorisés aux bâtiments. |
| `pvpMaxToPalDamage` | entier | `1000` | Dommages PvP maximum autorisés à Pals. |
| `pveMaxToPalBanThreshold` | entier | `900000` | PvE Pal-seuil de dégâts utilisé par la détection de triche. |
| `droppedPalPickupRange` | entier | `99999` | Distance maximale acceptée pour un ramassage abandonné-Pal. |
| `treeLimiter` | float | `0.1` | Secondes minimales entre les événements de destruction d'arbres utilisées pour limiter les éclats de feuillage. |
| `disableIllegalItemProtection` | bool | `false` | Désactive la protection des éléments invalid/modded. |
| `disableButchering` | bool | `false` | Bloque la boucherie Pal. |
| `disableRenaming` | bool | `false` | Bloque le renommage du joueur. |
| `disablePalRenaming` | bool | `false` | Bloque le renommage de Pal. |
| `doActionUponIllegalPalStats` | bool | `true` | Applique l'action de triche configurée pour les statistiques Pal impossibles. |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` | Bloque les recettes non prises en charge par l'atelier demandé. |
| `preventDoctorSurgiExploit` | bool | `true` | Detects/blocks l'exploit du Docteur Surgi. |
| `doActionUponDoctorSurgiExploit` | bool | `true` | Applique l'action de triche configurée pour cet exploit. |
| `palStatsMaxRank` | entier | `-1` | Rang d'amélioration maximum Pal ; `-1` utilise les limites de jeu automatic/current. |
| `bannedTechnologies` | array | Vide | ID technologiques bloqués lors de l'apprentissage et supprimés une fois détectés. |

## Commutateurs de fonction anti-triche

| Clé | Type | Par défaut | Descriptif |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` | Commutateur de compatibilité pour la fonctionnalité AntiDupe héritée ; inactif dans la version actuelle. |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` | Intervalle minimum hérité entre les builds ; actuellement inactif. |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` | Intervalle minimum hérité entre les démontages ; actuellement inactif. |
| `antiDupeShowBlockMessage` | bool | `true` | Commutateur de message de bloc hérité ; actuellement inactif. |
| `antiDupeBuildMessage` | string | Texte généré | Message de bloc de construction hérité ; actuellement inactif. |
| `antiDupeDismantleMessage` | string | Texte généré | Message de blocage de démantèlement hérité ; actuellement inactif. |
| `antiVacuumEnabled` | bool | `true` | Permet la protection du ramassage à distance (vide). |
| `antiVacuumBlockAutoPickup` | bool | `true` | Applique des contrôles anti-vide aux micros automatiques normaux. |
| `antiVacuumBlockRelicObtain` | bool | `true` | Applique les contrôles à la collection de reliques. |
| `antiVacuumBlockNoteObtain` | bool | `true` | Applique les contrôles à la collecte de notes. |
| `antiVacuumBlockEggPickup` | bool | `true` | Applique les chèques au ramassage des œufs. |
| `antiVacuumMaxPickupDistance` | float | `800.0` | Distance de prise en charge maximale autorisée pour les demandes protégées. |
| `antiVacuumShowBlockMessage` | bool | `true` | Affiche un message destiné au joueur lorsqu'un pick-up est bloqué. |
| `antiVacuumBlockMessage` | string | Texte généré | Message affiché pour un ramassage à distance bloqué. |
| `staminaCheatDetectionEnabled` | bool | `true` | Permet la détection d'actions d'endurance suspectes. |
| `baseCampDupeDetectionEnabled` | bool | `true` | Permet la détection de duplication de camp de base. |
| `damageCheatDetectionEnabled` | bool | `true` | Active la détection des tricheurs de dégâts. |
| `damageCheatDetectionTolerancePercent` | float | `5.0` | Différence en pourcentage autorisée entre les dommages natifs signalés et la valeur `BasePower × AttackWithBuff` reconstruite. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | float | `1.5` | Arme maximale autorisée `BasePower` en tant que multiplicateur du `AttackValue` statique de l'arme équipée. |
| `ammoCheatDetectionEnabled` | bool | `true` | Active la détection des triches liées aux munitions et à l'état de l'arme. |

Les clés `antiDupe...` sont toujours générées pour des raisons de compatibilité de configuration, mais la fonctionnalité AntiDupe héritée est désactivée dans la version actuelle. Ne comptez pas sur ces commandes jusqu'à ce que la fonctionnalité soit à nouveau activée.

## Clés de migration héritées

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS` et `PalImport_MaxIV` sont en lecture seule pour migrer des versions plus anciennes. installations à [`Pals/ImportRules/Default.json`](./PalImportRules.md). Ils ne sont plus écrits dans les fichiers `Config.json` actuels.

Les anciennes clés `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd` et `blockTowerBossCapture` ne font pas partie de la configuration actuelle. Les enregistrements d'interdiction appartiennent à `Banlist.json`.
