# 🛠️ `Config.json`

`Config.json` powstaje przy pierwszym uruchomieniu w `<PalServer>/Pal/Binaries/Win64/PalDefender/`. Przed edycją zatrzymaj serwer albo po zapisaniu zmian użyj `/reloadcfg`.

!!! note "Automatycznie zapisywane ustawienia"
    PalDefender zapisuje bieżący zestaw ustawień do tego pliku. Klucze niewymienione poniżej są przestarzałe, służą wyłącznie migracji lub nie są dostępne w obecnej publicznej kompilacji.

## Ustawienia ogólne i kary

| Klucz | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `version` | ciąg znaków | Bieżąca wersja | Znacznik schematu/wersji konfiguracji zarządzany przez PalDefender. |
| `MOTD` | tablica | Trzy wiadomości | Wiadomości powitalne. Obsługiwane zmienne: `{ServerName}`, `{PlayerName}`, `{Difficulty}`, `{DeathPenalty}`, `{AllowGlobalPalboxExport}`, `{AllowGlobalPalboxImport}`, `{IsPvP}`, `{IsHardcore}`, `{FriendlyFire}`, `{DayTimeSpeedRate}`, `{NightTimeSpeedRate}`, `{ExpRate}`, `{PalCaptureRate}`, `{PalSpawnNumRate}`, `{PalEggDefaultHatchingTime}`, `{EnemyDropItemRate}`, `{PalStomachDecreaceRate}`, `{PalStaminaDecreaceRate}`, `{BaseCampMaxNumInGuild}`, `{SupplyDropSpan}`, `{MaxBuildingLimitNum}`. |
| `exitServerOnStartupFailure` | wartość logiczna | `true` | Zatrzymuje serwer, jeśli PalDefender nie może się zainicjalizować. Niektóre hostingi mogą uznać to za awarię i wielokrotnie restartować serwer. |
| `preventAdminPasswordInChat` | wartość logiczna | `true` | Uniemożliwia wysłanie hasła administratora jako wiadomości czatu. |
| `shouldWarnCheaters` | wartość logiczna | `true` | Ostrzega gracza po automatycznym wykryciu oszustwa. |
| `shouldWarnCheatersReason` | wartość logiczna | `false` | Dodaje przyczynę wykrycia do ostrzeżenia. |
| `shouldKickCheaters` | wartość logiczna | `true` | Wyrzuca wykrytych oszustów, chyba że zastosowanie ma silniejsza włączona kara. |
| `shouldBanCheaters` | wartość logiczna | `false` | Banuje konta wykrytych oszustów. |
| `shouldIPBanCheaters` | wartość logiczna | `false` | Blokuje adresy IP wykrytych oszustów. |
| `blockEmergencyRespawn` | wartość logiczna | `true` | Blokuje akcję Menu → awaryjne odrodzenie. |

## RCON i logi

| Klucz | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `RCONTimeout` | liczba zmiennoprzecinkowa | `31.0` | Czas bezczynności połączenia RCON do jego zamknięcia, w sekundach. |
| `RCONbase64` | wartość logiczna | `false` | Włącza polecenia RCON kodowane w Base64. |
| `logNetworking` | wartość logiczna | `false` | Zapisuje obsługiwane logi sieciowe. W obecnej publicznej kompilacji logowanie sieci jest wyłączone. |
| `logNetworkingToConsole` | wartość logiczna | `true` | Wyświetla logi sieciowe także w konsoli, gdy funkcja jest dostępna. |
| `logChat` | wartość logiczna | `true` | Zapisuje czat globalny, gildii i lokalny (Say). |
| `logRCON` | wartość logiczna | `false` | Zapisuje polecenia RCON. |
| `logPlayerUID` | wartość logiczna | `false` | Dodaje PlayerUID do odpowiednich logów i webhooków ochrony przed oszustwami. |
| `logPlayerIP` | wartość logiczna | `true` | Dodaje adresy IP do odpowiednich logów i webhooków ochrony przed oszustwami. |
| `logPlayerDeaths` | wartość logiczna | `true` | Zapisuje zgony i zabójstwa graczy. |
| `logPlayerLogins` | wartość logiczna | `true` | Zapisuje dołączanie i opuszczanie serwera przez graczy. |
| `logPlayerBuildings` | wartość logiczna | `true` | Zapisuje obsługiwane akcje budowania, anulowania, rozbierania i przenoszenia Palboxa. |
| `logPlayerSummons` | wartość logiczna | `true` | Zapisuje przywołania bossów rajdowych przez graczy. |
| `logPlayerCaptures` | wartość logiczna | `true` | Ustawienie zachowane dla zgodności. W 1.9.0 logowanie schwytania jest wyłączone, ponieważ dostępne zdarzenie jest niewiarygodne. |
| `logPlayerDamage` | wartość logiczna | `false` | Zapisuje w konsoli serwera zdarzenia obrażeń zadanych przez graczy oraz zgłoszone oryginalne/bazowe wartości obrażeń. Działa niezależnie od wykrywania oszustw związanych z obrażeniami. |
| `BannedCampWorker` | tablica | Warianty Panthalus | Identyfikatory Character ID, których nie można przypisać do bazy. Wielkość liter nie ma znaczenia; warianty takie jak `BOSS_...` trzeba wymienić osobno. |
| `logHelicopterKills` | wartość logiczna | `true` | Zapisuje zniszczenia śmigłowców bojowych. |
| `logCraftings` | wartość logiczna | `true` | Zapisuje wytwarzanie przedmiotów przez graczy. |
| `logTechUnlocks` | wartość logiczna | `true` | Zapisuje odblokowanie technologii. |
| `logOpenOilrigBoxes` | wartość logiczna | `true` | Zapisuje zdarzenia końcowej skrzyni z nagrodami na platformie wiertniczej. |
| `OilrigGoalBoxLocktime` | liczba całkowita | `300` | Czas blokady końcowej skrzyni z nagrodami na platformie wiertniczej, w sekundach. |

## Webhooki Discorda

`PalWebhooks` jest obiektem. Pozostaw URL pusty, aby wyłączyć dany kanał wysyłania. Webhooki korzystają z kolejki, dzięki czemu nagromadzone wiadomości są wysyłane stopniowo i nie blokują wątku gry.

| Klucz zagnieżdżony | Wysyłane informacje |
| --- | --- |
| `webhookURL_Chat` | Wiadomości czatu globalnego i lokalnego (Say). |
| `webhookURL_GuildChat` | Wiadomości czatu gildii wraz z jej nazwą. |
| `webhookURL_Commands` | Polecenia wykonane przez czat w grze, wraz z administratorem i pełną treścią polecenia. |
| `webhookURL_Deaths` | Zgony i zabójstwa. Wymaga `announcePlayerDeaths` lub `logPlayerDeaths`. |
| `webhookURL_JoinLeave` | Dołączanie/opuszczanie serwera, gdy `announceConnections` jest włączone; uwzględnia `dontAnnounceAdminConnections`. |
| `webhookURL_Summons` | Ogłoszenia przywołań graczy/administratorów i pełne wyniki obrażeń dla przywołań z włączonym pomiarem. |
| `webhookURL_Oilrig` | Skrzynie na platformach wiertniczych i zniszczenia śmigłowców, gdy odpowiednie ustawienie `announce...` jest włączone. |
| `webhookURL_AntiCheats` | Automatyczne wykrycia oszustw i wykrycia wymagające ręcznej weryfikacji. Dodawanie UID/IP zależy od `logPlayerUID` i `logPlayerIP`. |

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

## Administracja, czat i ogłoszenia

| Klucz | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `useAdminWhitelist` | wartość logiczna | `true` | Ogranicza logowanie i polecenia administratora do `adminIPs`. |
| `adminAutoLogin` | wartość logiczna | `false` | Automatycznie włącza tryb administratora przy dołączeniu z dozwolonego IP. |
| `adminIPs` | tablica | `127.0.0.1` | Dokładne adresy IP i obsługiwane wzorce wieloznaczne uprawnione do administrowania serwerem. |
| `bannedChatWords` | tablica | Typowe określenia handlu za prawdziwe pieniądze | Słowa filtra czatu; wielkość liter nie ma znaczenia. |
| `bannedNames` | tablica | Znane nazwy używane do nadużyć | Nazwy graczy odrzucane podczas logowania. |
| `allowAdminCheats` | wartość logiczna | `false` | Pozwala administratorom używać poleceń z `adminCheats` i omijać wybrane zabezpieczenia. Sama broń administratora wymaga tylko aktywnych uprawnień administratora w grze. |
| `allowGodmodeOnehit` | wartość logiczna | `false` | Pozwala użytkownikom trybu nieśmiertelności zabijać jednym trafieniem. |
| `adminCheats` | tablica | Generowana lista | Polecenia uznawane za cheaty administratora, gdy `allowAdminCheats` jest wyłączone. Ta lista nie blokuje RCON. |
| `announceConnections` | wartość logiczna | `false` | Ogłasza dołączanie/opuszczanie serwera na czacie i włącza odpowiednie zdarzenia webhooka. |
| `dontAnnounceAdminConnections` | wartość logiczna | `true` | Ukrywa w tych ogłoszeniach dołączanie/opuszczanie serwera przez administratorów. |
| `announcePunishments` | wartość logiczna | `false` | Ogłasza automatyczne wyrzucenia/bany za oszustwa. |
| `announcePlayerDeaths` | wartość logiczna | `false` | Ogłasza zgony graczy na czacie. |
| `announceOpenOilrigBoxes` | wartość logiczna | `false` | Ogłasza zdarzenia skrzyń na platformach wiertniczych i włącza odpowiednie zdarzenia webhooka. |
| `announceHelicopterKills` | wartość logiczna | `false` | Ogłasza zniszczenia śmigłowców i włącza odpowiednie zdarzenia webhooka. |
| `announcePlayerSummons` | wartość logiczna | `false` | Ogłasza przywołania bossów rajdowych przez graczy. |
| `announceAdminSummons` | wartość logiczna | `false` | Ogłasza Pale utworzone przez funkcje przywoływania administratora. |
| `announceAdminSummonsKill` | wartość logiczna | `true` | Ogłasza zabójstwa/zgony Palów przywołanych przez administratora. |
| `chatBypassWait` | wartość logiczna | `true` | Usuwa standardowy czas oczekiwania między wiadomościami czatu. |
| `chatMessageMaxLen` | liczba całkowita | `128` | Maksymalna dozwolona długość wiadomości czatu. |
| `useWhitelist` | wartość logiczna | `false` | Włącza `WhiteList.json`. |
| `whitelistMessage` | ciąg znaków | Generowany tekst | Wiadomość dla gracza, któremu odmówiono dostępu z powodu braku na liście dozwolonych. |
| `steamidProtection` | wartość logiczna | `true` | Odrzuca jednoczesne użycie tego samego UserId przez więcej niż jedno połączenie. |

## Weryfikacja rozgrywki

| Klucz | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `pvpMaxToBuildingDamage` | liczba całkowita | `100` | Maksymalne dozwolone obrażenia PvP zadawane budynkom. |
| `pvpMaxToPalDamage` | liczba całkowita | `1000` | Maksymalne dozwolone obrażenia PvP zadawane Palom. |
| `pveMaxToPalBanThreshold` | liczba całkowita | `900000` | Próg obrażeń PvE zadanych Palom używany do wykrywania oszustw. |
| `droppedPalPickupRange` | liczba całkowita | `99999` | Maksymalna dozwolona odległość podnoszenia upuszczonego Pala. |
| `treeLimiter` | liczba zmiennoprzecinkowa | `0.1` | Minimalny odstęp w sekundach między zniszczeniami drzew, ograniczający masowe niszczenie roślinności. |
| `disableIllegalItemProtection` | wartość logiczna | `false` | Wyłącza ochronę przed nieprawidłowymi/zmodyfikowanymi przedmiotami. |
| `disableButchering` | wartość logiczna | `false` | Blokuje ubój Palów. |
| `disableRenaming` | wartość logiczna | `false` | Blokuje zmianę nazw graczy. |
| `disablePalRenaming` | wartość logiczna | `false` | Blokuje zmianę nazw Palów. |
| `doActionUponIllegalPalStats` | wartość logiczna | `true` | Stosuje skonfigurowaną karę za niemożliwe statystyki Pala. |
| `preventUnsupportedWorkbenchRecipes` | wartość logiczna | `true` | Blokuje receptury nieobsługiwane przez dane stanowisko rzemieślnicze. |
| `preventDoctorSurgiExploit` | wartość logiczna | `true` | Wykrywa/blokuje nadużycie błędu związanego z Doctor Surgi. |
| `doActionUponDoctorSurgiExploit` | wartość logiczna | `true` | Stosuje skonfigurowaną karę za to nadużycie. |
| `palStatsMaxRank` | liczba całkowita | `-1` | Maksymalny poziom wzmocnienia Pala; `-1` automatycznie stosuje aktualne limity gry. |
| `bannedTechnologies` | tablica | Brak | Identyfikatory technologii, których nauka jest blokowana i które są usuwane po wykryciu. |

## Przełączniki ochrony przed oszustwami

| Klucz | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `antiDupeEnabled` | wartość logiczna | `true` | Przełącznik zgodności starszej funkcji AntiDupe; nie działa w obecnym wydaniu. |
| `antiDupeBuildRateLimitSeconds` | liczba zmiennoprzecinkowa | `1.5` | Dawny minimalny odstęp między akcjami budowania; obecnie nieaktywny. |
| `antiDupeDismantleRateLimitSeconds` | liczba zmiennoprzecinkowa | `1.5` | Dawny minimalny odstęp między rozbieraniem; obecnie nieaktywny. |
| `antiDupeShowBlockMessage` | wartość logiczna | `true` | Dawny przełącznik komunikatu blokady; obecnie nieaktywny. |
| `antiDupeBuildMessage` | ciąg znaków | Generowany tekst | Dawny komunikat blokady budowania; obecnie nieaktywny. |
| `antiDupeDismantleMessage` | ciąg znaków | Generowany tekst | Dawny komunikat blokady rozbierania; obecnie nieaktywny. |
| `antiVacuumEnabled` | wartość logiczna | `true` | Włącza ochronę przed zbieraniem na odległość (vacuum). |
| `antiVacuumBlockAutoPickup` | wartość logiczna | `true` | Stosuje kontrole Anti-Vacuum do zwykłego automatycznego zbierania. |
| `antiVacuumBlockRelicObtain` | wartość logiczna | `true` | Stosuje kontrole do zbierania reliktów. |
| `antiVacuumBlockNoteObtain` | wartość logiczna | `true` | Stosuje kontrole do zbierania notatek. |
| `antiVacuumBlockEggPickup` | wartość logiczna | `true` | Stosuje kontrole do zbierania jaj. |
| `antiVacuumMaxPickupDistance` | liczba zmiennoprzecinkowa | `800.0` | Maksymalna dozwolona odległość zbierania dla chronionych żądań. |
| `antiVacuumShowBlockMessage` | wartość logiczna | `true` | Wyświetla graczowi komunikat po zablokowaniu zbierania. |
| `antiVacuumBlockMessage` | ciąg znaków | Generowany tekst | Komunikat po zablokowaniu zbierania na odległość. |
| `staminaCheatDetectionEnabled` | wartość logiczna | `true` | Włącza wykrywanie podejrzanych akcji związanych z wytrzymałością. |
| `baseCampDupeDetectionEnabled` | wartość logiczna | `true` | Włącza wykrywanie duplikowania baz. |
| `damageCheatDetectionEnabled` | wartość logiczna | `true` | Włącza wykrywanie oszustw związanych z obrażeniami. |
| `damageCheatDetectionTolerancePercent` | liczba zmiennoprzecinkowa | `5.0` | Dopuszczalna różnica procentowa między zgłoszonymi oryginalnymi obrażeniami a odtworzoną wartością `BasePower × AttackWithBuff`. |
| `damageCheatDetectionWeaponBasePowerMultiplier` | liczba zmiennoprzecinkowa | `1.5` | Maksymalne dozwolone `BasePower` broni jako mnożnik statycznej wartości `AttackValue` wyposażonej broni. |
| `ammoCheatDetectionEnabled` | wartość logiczna | `true` | Włącza wykrywanie oszustw związanych z amunicją i stanem broni. |

Klucze `antiDupe...` nadal są generowane dla zgodności konfiguracji, ale starsza funkcja AntiDupe jest wyłączona w obecnym wydaniu. Nie polegaj na tych ustawieniach, dopóki funkcja nie zostanie ponownie włączona.

## Klucze migracji starszych ustawień

`PalImport_Disabled`, `PalImport_BanIfPalIsImpossible`, `PalImport_BannedPalIDs`, `PalImport_AllowGenderNone`, `PalImport_MaxLevel`, `PalImport_MaxRank`, `PalImport_MaxSoulHP`, `PalImport_MaxSoulATK`, `PalImport_MaxSoulDEF`, `PalImport_MaxSoulCS` i `PalImport_MaxIV` są odczytywane wyłącznie przy migracji starszych instalacji do [`Pals/ImportRules/Default.json`](./PalImportRules.md). Nie są już zapisywane w obecnych plikach `Config.json`.

Dawne `RCONUsePacketIdFix`, `bannedIPs`, `bannedMessage`, `isChineseCmd` i `blockTowerBossCapture` nie należą do obecnej konfiguracji. Bany są przechowywane w `Banlist.json`.
