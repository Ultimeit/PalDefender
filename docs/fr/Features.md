# Caractéristiques et état actuel

Cette page résume les commutateurs de fonctionnalités destinés à l'utilisateur dans PalDefender 1.9.1. Pour connaître les valeurs par défaut exactes, voir [`Config.json`](./FileTypes/Config.md).

## Protection active

- Les détections de dégâts, d'endurance, de munitions et de duplication du camp de base peuvent être commutées indépendamment.
- Anti-Vacuum bloque les tentatives suspectes de récupération à distance d'objets ordinaires, d'œufs Pal, de reliques et de notes. Les administrateurs contournent les vérifications prises en charge lorsque `allowAdminCheats` est activé.
- Les éléments non valides, Pal-stat, la recette de l'établi, le docteur Surgi, la réapparition d'urgence et d'autres contrôles d'action du serveur font toujours partie de la couche de validation centrale.
- `BannedCampWorker` empêche l'attribution des ID de personnage configurés à une base.

La fonctionnalité héritée contrôlée par les clés `antiDupe...` est compilée à partir de la version actuelle. Le nouveau détecteur de duplication du camp de base est séparé et contrôlé par `baseCampDupeDetectionEnabled`.

## Administration et événements

- `/admingun` (`/agun`) donne l’[Admin Gun](./Commands/index.md) protégée à un administrateur actif dans le jeu.
- `/setting` peut inspecter ou modifier temporairement les paramètres Palworld en direct pris en charge.
- `/findbases` fournit une file d'attente de révision interactive pour les bases empty/inactive.
- PalSummons prend en charge les noms de rencontre, les contrôles AI/damage-meter, les multiplicateurs de statistiques, la capture conditionnelle, les résultats de classement et les récompenses configurables. Voir [`PalSummon.json`](./FileTypes/PalSummon.md).
- Les destinations Discord sont configurées sous `PalWebhooks` et couvrent le chat, les commandes, les décès, joins/leaves, les invocations, les événements de plate-forme pétrolière et les détections anti-triche.

## Battement de coeur

Les versions de version envoient un battement de cœur à `https://pallink.net/api/heartbeat` toutes les 10 secondes une fois le jeu prêt. Sa charge utile contient le world/server GUID, le code pays du système d'exploitation, les versions PalDefender et Palworld, la plate-forme Windows/Wine/Proton, la disponibilité du processus et le nombre de joueurs online/maximum/unique-total. Il n'inclut pas les noms des joueurs, les identifiants de compte de joueur, les adresses IP des joueurs, les messages de discussion ou le contenu des sauvegardes. Il est exclu des versions de débogage.

## REST API

Le REST API authentifié prend en charge les flux de travail du joueur, Pal, de l'inventaire, de la technologie, de la progression, de la guilde, du bannissement, de la messagerie, des récompenses et de la modération. La version 1.9.0 ajoute également [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) et [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md).
