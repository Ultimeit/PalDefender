# 🛠️ `Config.json`

`Config.json` генерируется в `<PalServer>/Pal/Binaries/Win64/PalDefender/` при первом запуске. Остановите сервер перед его редактированием или используйте `/reloadcfg` после сохранения изменений.

!!! note "Сгенерированные настройки"
    PalDefender записывает текущий набор настроек обратно в этот файл. Ключи, не перечисленные ниже, являются устаревшими, предназначены только для миграции или недоступны в текущей общедоступной сборке.

## Общие положения и правоприменение

| Ключ | Тип | По умолчанию | Описание |
| --- | --- | --- | --- |
| `version` | string | Текущая версия | Маркер конфигурации schema/version поддерживается PalDefender. |
| `MOTD` | array | Три сообщения | Присоединяйтесь к сообщениям. Поддерживает `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}` и `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | bool | `true` | Останавливает сервер, если PalDefender не может инициализироваться. Некоторые хосты могут интерпретировать это как сбой и неоднократно перезагружаться. |
| `preventAdminPasswordInChat` | bool | `true` | Блокирует отправку пароля администратора в виде текста в чате. |
| `shouldWarnCheaters` | bool | `true` | Предупреждает игрока о срабатывании автоматического обнаружения. |
| `shouldWarnCheatersReason` | bool | `false` | Включает причину обнаружения в это предупреждение. |
| `shouldKickCheaters` | bool | `true` | Кики обнаруживают мошенников, если не применяется более сильное действие. |
| `shouldBanCheaters` | bool | `false` | Баны аккаунтов выявили мошенников. |
| `shouldIPBanCheaters` | bool | `false` | IP-баны выявили мошенников. |
| `blockEmergencyRespawn` | bool | `true` | Блокирует меню → Действие «Аварийное возрождение». |

## RCON и ведение журнала

| Ключ | Тип | По умолчанию | Описание |
| --- | --- | --- | --- |
| `RCONTimeout` | float | `31.0` | За несколько секунд до истечения времени ожидания неактивного соединения RCON. |
| `RCONbase64` | bool | `false` | Включает команды RCON в кодировке Base64. |
| `logNetworking` | bool | `false` | Записывает поддерживаемое сетевое журналирование. Ведение журнала сети отключено в текущей общедоступной сборке. |
| `logNetworkingToConsole` | bool | `true` | Зеркально отображает сетевые журналы на консоли, если сетевые журналы доступны. |
| `logChat` | bool | `true` | Регистрирует глобальный, гильдейский и чат-чат. |
| `logRCON` | bool | `false` | Регистрирует команды RCON. |
| `logPlayerUID` | bool | `false` | Включает PlayerUID в соответствующие журналы и веб-перехватчики для защиты от мошенничества. |
| `logPlayerIP` | bool | `true` | Включает IP-адреса в соответствующие журналы и веб-перехватчики для защиты от мошенничества. |
| `logPlayerDeaths` | bool | `true` | Регистрирует смерти и убийства игроков. |
| `logPlayerLogins` | bool | `true` | Регистрирует присоединение и выход игрока. |
| `logPlayerBuildings` | bool | `true` | Журналы поддерживают сборку, отмену, демонтаж и перемещение Palbox. |
| `logPlayerSummons` | bool | `true` | Регистрирует вызовы рейд-боссов игроков. |
| `logPlayerCaptures` | bool | `true` | Зарезервированная настройка совместимости. Ведение журнала захвата отключено в версии 1.9.0, поскольку доступное событие ненадежно. |
| `logPlayerDamage` | bool | `false` | Регистрирует события повреждений, вызванные действиями игрока, и сообщаемые ими значения ущерба native/base на консоли сервера. Работает независимо от обнаружения повреждений. |
| `BannedCampWorker` | array | Варианты Панталуса | Идентификаторы персонажей, которые нельзя назначить на базе. Сопоставление не учитывает регистр; такие варианты, как `BOSS_...`, должны быть указаны отдельно. |
| `logHelicopterKills` | bool | `true` | Журналы убийств боевых вертолетов. |
| `logCraftings` | bool | `true` | Журналы создания игроков. |
| `logTechUnlocks` | bool | `true` | Технология журналов разблокируется. |
| `logOpenOilrigBoxes` | bool | `true` | Регистрирует события в поле для ворот на нефтяной вышке. |
| `OilrigGoalBoxLocktime` | интервал | `300` | Секунды на конце ворот нефтяной вышки остаются заблокированными. |

## Discord веб-перехватчики

`PalWebhooks` — это object. Оставьте отдельный URL-адрес пустым, чтобы отключить этот пункт назначения. Доставка Webhook ставится в очередь, поэтому пакеты распределяются в шахматном порядке, а не блокируют игровой поток.

| Вложенный ключ | Отправляет |
| --- | --- |
| `webhookURL_Chat` | Сообщения чата Global и Say. |
| `webhookURL_GuildChat` | Сообщения в чате гильдии с названием гильдии. |
| `webhookURL_Commands` | Команды запускаются через внутриигровой чат, включая администратора и полное командование. |
| `webhookURL_Deaths` | Смерти и убийства. Требуется `announcePlayerDeaths` или `logPlayerDeaths`. |
| `webhookURL_JoinLeave` | События Join/leave при включении `announceConnections`; уважает `dontAnnounceAdminConnections`. |
| `webhookURL_Summons` | Player/admin объявления о призыве и полные результаты отслеживания урона. |
| `webhookURL_Oilrig` | Коробки нефтяных вышек и убийства вертолетов, если включена соответствующая настройка `announce...`. |
| `webhookURL_AntiCheats` | Автоматическое и ручное обнаружение античитов. Включение UID/IP следует за `logPlayerUID` и `logPlayerIP`. |

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

## Администрация, чат и объявления

| Ключ | Тип | По умолчанию | Описание |
| --- | --- | --- | --- |
| `useAdminWhitelist` | bool | `true` | Ограничивает администратора login/commands до `adminIPs`. |
| `adminAutoLogin` | bool | `false` | Автоматически включает режим администратора для присоединяющегося IP-адреса из белого списка. |
| `adminIPs` | array | `127.0.0.1` | Точные IP-адреса и поддерживаемые подстановочные знаки позволяют администрировать сервер. |
| `bannedChatWords` | array | Общие термины РМТ | Условия фильтрации чата без учета регистра. |
| `bannedNames` | array | Известные имена злоупотреблений | Имена игроков отклонены при входе в систему. |
| `allowAdminCheats` | bool | `false` | Позволяет администраторам использовать команды в `adminCheats` и обходить выбранные средства защиты. Для самого Admin Gun требуется только активный статус игрового администратора. |
| `allowGodmodeOnehit` | bool | `false` | Позволяет пользователям режима Бога наносить урон одним ударом. |
| `adminCheats` | array | Сгенерированный список | Команды, рассматриваемые как читы администратора, когда `allowAdminCheats` отключен. RCON не заблокирован этим списком. |
| `announceConnections` | bool | `false` | Объявляет joins/leaves в чате и включает источник веб-перехватчика join/leave. |
| `dontAnnounceAdminConnections` | bool | `true` | Скрывает администратора joins/leaves из этих объявлений. |
| `announcePunishments` | bool | `false` | Объявляет автоматический чит kicks/bans. |
| `announcePlayerDeaths` | bool | `false` | Сообщает о смерти игрока в чате. |
| `announceOpenOilrigBoxes` | bool | `false` | Объявляет события коробки Oil Rig и включает их источник веб-перехватчиков. |
| `announceHelicopterKills` | bool | `false` | Объявляет о убийстве вертолета и включает источник веб-перехватчика. |
| `announcePlayerSummons` | bool | `false` | Объявляет о вызове рейд-босса игрока. |
| `announceAdminSummons` | bool | `false` | Объявляет, что Pals создается с помощью функций административного вызова. |
| `announceAdminSummonsKill` | bool | `true` | Объявляет kills/deaths об административном вызове Pals. |
| `chatBypassWait` | bool | `true` | Удаляет обычное ожидание в чате между сообщениями. |
| `chatMessageMaxLen` | интервал | `128` | Максимальная допустимая длина сообщения чата. |
| `useWhitelist` | bool | `false` | Включает `WhiteList.json`. |
| `whitelistMessage` | string | Сгенерированный текст | Сообщение, отображаемое отклоненному игроку, не внесенному в белый список. |
| `steamidProtection` | bool | `true` | Отклоняет повторное одновременное использование UserId. |

## Проверка игрового процесса

| Ключ | Тип | По умолчанию | Описание |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | интервал | `100` | Максимально допустимое повреждение зданий PvP. |
| `pvpMaxToPalDamage` | интервал | `1000` | Максимально допустимое повреждение PvP Pals. |
| `pveMaxToPalBanThreshold` | интервал | `900000` | PvE Pal — порог урона, используемый при обнаружении читов. |
| `droppedPalPickupRange` | интервал | `99999` | Максимально допустимое расстояние для брошенного пикапа-Pal. |
| `treeLimiter` | float | `0.1` | Минимальное количество секунд между событиями уничтожения деревьев, используемое для ограничения разрывов листвы. |
| `disableIllegalItemProtection` | bool | `false` | Отключает защиту элемента invalid/modded. |
| `disableButchering` | bool | `false` | Блокирует разделку Pal. |
| `disableRenaming` | bool | `false` | Блокирует переименование игрока. |
| `disablePalRenaming` | bool | `false` | Блокирует переименование Pal. |
| `doActionUponIllegalPalStats` | bool | `true` | Применяет настроенное чит-действие для невозможной статистики Pal. |
| `preventUnsupportedWorkbenchRecipes` | bool | `true` | Блокирует рецепты, не поддерживаемые запрошенной рабочей средой. |
| `preventDoctorSurgiExploit` | bool | `true` | Detects/blocks эксплойт Doctor Surgi. |
| `doActionUponDoctorSurgiExploit` | bool | `true` | Применяет настроенное чит-действие для этого эксплойта. |
| `palStatsMaxRank` | интервал | `-1` | Максимальный ранг улучшения Pal; `-1` использует игровые ограничения automatic/current. |
| `bannedTechnologies` | array | Пусто | Идентификаторы технологий заблокированы для изучения и удалены при обнаружении. |

## Переключатели функций защиты от мошенничества

| Ключ | Тип | По умолчанию | Описание |
| --- | --- | --- | --- |
| `antiDupeEnabled` | bool | `true` | Переключатель совместимости для устаревшей функции AntiDupe; неактивен в текущей сборке выпуска. |
| `antiDupeBuildRateLimitSeconds` | float | `1.5` | Устаревший минимальный интервал между сборками; в настоящее время неактивен. |
| `antiDupeDismantleRateLimitSeconds` | float | `1.5` | Устаревший минимальный интервал между демонтажами; в настоящее время неактивен. |
| `antiDupeShowBlockMessage` | bool | `true` | Устаревший переключатель блокировки сообщений; в настоящее время неактивен. |
| `antiDupeBuildMessage` | string | Сгенерированный текст | Устаревшее сообщение о блокировке сборки; в настоящее время неактивен. |
| `antiDupeDismantleMessage` | string | Сгенерированный текст | Устаревшее сообщение о блокировке демонтажа; в настоящее время неактивен. |
| `antiVacuumEnabled` | bool | `true` | Включает защиту удаленного захвата (вакуума). |
| `antiVacuumBlockAutoPickup` | bool | `true` | Применяет антивакуумные проверки к обычным автозахватам. |
| `antiVacuumBlockRelicObtain` | bool | `true` | Применяет проверки к сбору реликвий. |
| `antiVacuumBlockNoteObtain` | bool | `true` | Применяет проверки к сбору заметок. |
| `antiVacuumBlockEggPickup` | bool | `true` | Применяет проверки при сборе яиц. |
| `antiVacuumMaxPickupDistance` | float | `800.0` | Максимально допустимое расстояние ответа для защищенных запросов. |
| `antiVacuumShowBlockMessage` | bool | `true` | Показывает сообщение игроку, когда получение заблокировано. |
| `antiVacuumBlockMessage` | string | Сгенерированный текст | Сообщение отображается для заблокированного удаленного ответа. |
| `staminaCheatDetectionEnabled` | bool | `true` | Включает обнаружение подозрительных действий выносливости. |
| `baseCampDupeDetectionEnabled` | bool | `true` | Включает обнаружение дублирования базового лагеря. |
| `damageCheatDetectionEnabled` | bool | `true` | Включает обнаружение чит-повреждений. |
| `damageCheatDetectionTolerancePercent` | float | `5.0` | Допустимая процентная разница между зарегистрированным естественным повреждением и реконструированным значением `BasePower × AttackWithBuff`. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | float | `1.5` | Максимально разрешенное оружие `BasePower` как множитель статического значения `AttackValue` экипированного оружия. |
| `ammoCheatDetectionEnabled` | bool | `true` | Включает обнаружение читов, связанных с боеприпасами и состоянием оружия. |

Ключи `antiDupe...` по-прежнему генерируются для совместимости конфигурации, но устаревшая функция AntiDupe отключена в текущей сборке выпуска. Не полагайтесь на эти элементы управления, пока эта функция не будет снова включена.

## Устаревшие ключи миграции

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS` и `PalImport_MaxIV` доступны только для чтения при переходе на старые версии установки на [`Pals/ImportRules/Default.json`](./PalImportRules.md). Они больше не записываются в текущие файлы `Config.json`.

Старые ключи `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd` и `blockTowerBossCapture` не являются частью текущей конфигурации. Записи о запрете относятся к `Banlist.json`.
