# 📄 `PalTemplate.json`

Skorzystaj z <https://paldeck.cc/creator>, aby znacznie łatwiej tworzyć te pliki!

!!! tip "Wyszukiwanie identyfikatorów"
    `PalID` znajdziesz na [paldeck.cc/pals](https://paldeck.cc/pals), `Passives` na [paldeck.cc/passives](https://paldeck.cc/passives), a `ActiveSkills` i `LearntSkills` na [paldeck.cc/skills](https://paldeck.cc/skills).

| Klucz | Typ | Opis |
| ------------------------ | ------ | ----------------------------------------------------------------------------------- |
| `PalID`                  | ciąg znaków | Wewnętrzny identyfikator tworzonego Pala. Prawidłowe [`PalID`](https://paldeck.cc/pals) znajdziesz na Paldeck. |
| `UniqueNPCID`            | ciąg znaków | Wewnętrzny identyfikator używany przy tworzeniu NPC.                                               |
| `Nickname`               | ciąg znaków | Opcjonalny pseudonim Pala.                                                 |
| `SkinId`                 | ciąg znaków | Zmiana skórki Pala, pozwalająca dostosować wygląd. Pobierz identyfikatory poleceniem `/getskinids`. |
| `Gender`                 | ciąg znaków | `"Male"` (samiec), `"Female"` (samica) lub `"None"` (brak).                                                   |
| `Level`                  | liczba całkowita | Poziom Pala.                                                               |
| `Exp`                    | liczba całkowita | Punkty doświadczenia.                                                                  |
| `Shiny`                  | wartość logiczna | Czy Pal jest rzadki (shiny).                                                           |
| `PartnerSkillLevel`      | liczba całkowita | Poziom umiejętności partnerskiej Pala. Musi wynosić co najmniej 1!                           |
| `CondensedPals`          | liczba całkowita | Liczba Palów użytych do kondensacji tego Pala.                                      |
| `UnusedStatusPoints`     | liczba całkowita | Niewydane punkty statystyk do ręcznego przydzielenia. Prawdopodobnie używane tylko dla graczy.    |
| `FriendshipPoints`       | liczba całkowita | Wartość przyjaźni Pala.                                               |
| `PhysicalHealth`         | ciąg znaków | Stan zdrowia fizycznego. Prawidłowe nazwy to: `Healthful`, `MinorInjury`, `Severe`, `Dying`, `DeadBody`, `CloudCemetery`. |
| `WorkerSick`             | ciąg znaków | Stan choroby pracującego Pala. Prawidłowe nazwy to: `None`, `Cold`, `Sprain`, `Bulimia`, `GastricUlcer`, `Fracture`, `Weakness`, `DepressionSprain`, `DisturbingElement`. |
| `ImportedCharacter`      | wartość logiczna | Oznacza Pala jako zaimportowaną postać.                                    |
| `HP` / `SP` / `MP`       | liczba | Bazowe wartości zdrowia, wytrzymałości i many. `HP` określa maksymalne zdrowie tworzonego Pala, także w przywołaniach PalSummon i REST odwołujących się do tego szablonu. |
| `Shield`                 | liczba | Wartość osłony.                                                              |
| `Hunger` / `MaxHunger`   | liczba całkowita | Bieżąca i maksymalna sytość.                                                      |
| `SAN`                    | liczba całkowita | SAN (stabilność psychiczna Pala).                                               |
| `Support`                | liczba całkowita | Poziom wsparcia używany przez AI i umiejętności.                                    |
| `CraftSpeed`             | liczba całkowita | Mnożnik szybkości wytwarzania.                                                          |
| `PalSouls`               | obiekt | Bonusy ze wzmocnienia duszami. Zawiera: `Health`, `Attack`, `Defense`, `CraftSpeed`. Zalecane standardowe wartości są kontrolowane przez reguły importu. |
| `IVs`                    | obiekt | Wartości indywidualne statystyk (IV). Zawiera: `Health`, `AttackMelee`, `AttackShot`, `Defense`. Zalecane standardowe wartości są kontrolowane przez reguły importu. |
| `ActiveSkills`           | tablica | Lista wyposażonych umiejętności. PalDefender 1.9.0 nie ogranicza szablonów administratora do trzech wpisów; wszystkie pozostają wyposażone. Prawidłowe [ID umiejętności](https://paldeck.cc/skills) znajdziesz na Paldeck. Gra i interfejs mogą nadal zakładać standardową liczbę slotów. |
| `LearntSkills`           | tablica | Umiejętności, których Pal się nauczył i na które może przełączyć ataki. Nie umieszczaj tutaj aktualnie wyposażonych ataków. Prawidłowe [ID umiejętności](https://paldeck.cc/skills) znajdziesz na Paldeck. |
| `Passives`               | tablica | Cechy pasywne Pala. Zwykłe Pale powinny mieć najwyżej 4. Prawidłowe [`PassiveID`](https://paldeck.cc/passives) znajdziesz na Paldeck. |
| `ExtraWorkSuitabilities` | obiekt | Wzmocnione rodzaje pracy i poziomy (np. `"Mining": 2`). Dostępne rodzaje pracy: `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`.  |
| `DisableWorkPreferences` | tablica | Rodzaje pracy, których Pal nie wykonuje. Dostępne rodzaje pracy: `BaseCampBattle`, `EmitFlame`, `Watering`, `Seeding`, `GenerateElectricity`, `Handcraft`, `Collection`, `Deforest`, `Mining`, `OilExtraction`, `ProductMedicine`, `Cool`, `Transport`, `MonsterFarm`. |

## Zasady przygotowania

1. Utwórz osobny plik JSON dla każdego niestandardowego Pala w `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
2. Użyj unikalnej nazwy, np. `RaidRewardAnubis.json`. W poleceniach zwykle można podać `RaidRewardAnubis` lub `RaidRewardAnubis.json`.
3. Zawsze dodaj `PalID`. Pozostałe pola są opcjonalne; pominięte wartości korzystają z ustawień domyślnych PalDefender lub Palworld.
4. Ustaw `Level` i `PartnerSkillLevel` na co najmniej `1`.
5. Wyposażone ataki umieść w `ActiveSkills`, a pozostałe znane ataki w `LearntSkills`. PalDefender nie przenosi już nadmiarowych aktywnych wpisów do wyuczonych umiejętności.
6. Używaj dokładnych ID Palów, umiejętności, cech pasywnych, skórek i rodzajów pracy. Błędne ID mogą spowodować odrzucenie importu lub zostać zignorowane.
7. Sprawdź JSON przed przesłaniem. JSON nie dopuszcza komentarzy ani przecinków po ostatnich elementach.
8. Jeśli import zmienia lub blokuje wartości, sprawdź `Pals/ImportRules/Default.json` serwera i pliki wyjątków dla danego Pala.

## Konfiguracja krok po kroku

1. Określ cel szablonu: prosta nagroda administratora, boss wydarzenia, Pal testowy lub szablon tworzenia przywołania.
2. Wybierz `PalID` na [paldeck.cc/pals](https://paldeck.cc/pals). Wyświetlana nazwa nie zawsze jest ID używanym w pliku, więc skopiuj ID dokładnie.
3. Dodaj tylko pola, które chcesz ustawić. W krótkim szablonie łatwiej znaleźć błędy.
4. Wybierz umiejętności na [paldeck.cc/skills](https://paldeck.cc/skills). Wyposażone ataki umieść w `ActiveSkills`, a pozostałe wyuczone ataki w `LearntSkills`.
5. Wybierz cechy pasywne na [paldeck.cc/passives](https://paldeck.cc/passives). Zwykle używaj najwyżej czterech, chyba że serwer celowo dopuszcza więcej.
6. Zapisz plik w `Pal/Binaries/Win64/PalDefender/Pals/Templates/`.
7. Najpierw przetestuj `/givemepal_j <filename>`. Następnie użyj tego samego szablonu w `/givepal_j`, `/spawnpal_j`, `/giveegg_j`, REST API lub `PalSummon.json`.

## Objaśnienie przykładów

Minimalny przykład poniżej tworzy Anubisa na poziomie 50 z trzema wyposażonymi atakami i dwiema cechami pasywnymi. Nadaje się do testów, ponieważ zawiera tylko wymagane `PalID` i kilka typowych pól.

Rozbudowany przykład celowo używa skrajnych wartości. Pokazuje strukturę dusz, IV, umiejętności, cech pasywnych i zmian predyspozycji do pracy. Na serwerach z regułami importu wysokie wartości mogą zostać obniżone lub zablokowane.

## Minimalny przykład

```json
{
    "PalID": "Anubis",
    "Nickname": "Anubis z areny",
    "Gender": "None",
    "Level": 50,
    "PartnerSkillLevel": 1,
    "HP": 3500,
    "SAN": 100,
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "RockLance"
    ],
    "Passives": [
        "Legend",
        "CraftSpeed_up3"
    ]
}
```

## Przykład

Ten plik należy zapisać w: `<...>/Pal/Binaries/Win64/PalDefender/Pals/Templates/ExamplePalTemplate.json`
(`ExamplePalTemplate` można zastąpić dowolną unikalną nazwą w tym folderze. Będzie ona argumentem poleceń `/givepal_j` i `/spawnpal_j`!)

```json
{
    "PalID": "Anubis",
    "Nickname": "SuperAnubis",
    "Gender": "None",
    "Level": 255,
    "Shiny": true,
    "PartnerSkillLevel": 255,
    "HP": 999999,
    "SP": 999999,
    "MP": 999999,
    "Hunger": 999999,
    "MaxHunger": 999999,
    "SAN": 999999,
    "Support": 999999,
    "CraftSpeed": 999999,
    "PalSouls": {
        "Health": 255,
        "Attack": 255,
        "Defense": 255,
        "CraftSpeed": 255
    },
    "IVs": {
        "Health": 255,
        "AttackMelee": 255,
        "AttackShot": 255,
        "Defense": 255
    },
    "ActiveSkills": [
        "SandTornado",
        "Unique_Anubis_GroundPunch",
        "Unique_Anubis_LowRoundKick"
    ],
    "Passives": [
        "Legend",
        "PAL_ALLAttack_up3",
        "Deffence_up3",
        "Vampire",
        "Stamina_Up_3",
        "EternalFlame",
        "PAL_Sanity_Down_3",
        "Invader",
        "SwimSpeed_up_3",
        "Rare",
        "Nushi",
        "PAL_FullStomach_Down_3",
        "CraftSpeed_up3",
        "Salvation",
        "Witch",
        "MoveSpeed_up_3",
        "SwimSpeed_up_2",
        "CraftSpeed_up2",
        "Deffence_up2",
        "ElementBoost_Normal_2_PAL",
        "PAL_FullStomach_Down_2",
        "ElementBoost_Dragon_2_PAL",
        "ElementBoost_Earth_2_PAL",
        "PAL_ALLAttack_up2",
        "ElementBoost_Fire_2_PAL",
        "ElementBoost_Ice_2_PAL",
        "Stamina_Up_1",
        "TrainerLogging_up1",
        "ElementBoost_Thunder_2_PAL",
        "ElementBoost_Aqua_2_PAL",
        "ElementBoost_Dark_2_PAL",
        "TrainerMining_up1",
        "TrainerWorkSpeed_UP_1",
        "SalePrice_Up_1",
        "Test_PalEgg_HatchingSpeed_Up",
        "MoveSpeed_up_2",
        "CoolTimeReduction_Up_1",
        "ElementBoost_Leaf_2_PAL",
        "TrainerDEF_UP_1",
        "TrainerATK_UP_1",
        "PAL_Sanity_Down_2",
        "ElementResist_Normal_1_PAL",
        "ElementBoost_Dragon_1_PAL",
        "ElementResist_Leaf_1_PAL",
        "PAL_ALLAttack_up1",
        "ElementBoost_Thunder_1_PAL",
        "ElementResist_Dark_1_PAL",
        "ElementBoost_Ice_1_PAL",
        "PAL_FullStomach_Down_1",
        "ElementResist_Dragon_1_PAL",
        "ElementResist_Earth_1_PAL",
        "SalePrice_Up_2",
        "Stamina_Up_2",
        "ElementBoost_Leaf_1_PAL",
        "Deffence_up1",
        "ElementResist_Ice_1_PAL",
        "ElementBoost_Aqua_1_PAL",
        "CoolTimeReduction_Up_2",
        "ElementResist_Thunder_1_PAL",
        "MoveSpeed_up_1",
        "Alien",
        "PAL_Sanity_Down_1",
        "ElementBoost_Earth_1_PAL",
        "ElementBoost_Fire_1_PAL",
        "CraftSpeed_up1",
        "SwimSpeed_up_1",
        "ElementResist_Fire_1_PAL",
        "ElementBoost_Dark_1_PAL",
        "ElementResist_Aqua_1_PAL",
        "ElementBoost_Normal_1_PAL"
    ],
    "ExtraWorkSuitabilities": {
        "EmitFlame": 5,
        "Watering": 5,
        "Seeding": 5,
        "GenerateElectricity": 5,
        "Handcraft": 5,
        "Collection": 5,
        "Deforest": 5,
        "Mining": 5,
        "OilExtraction": 5,
        "ProductMedicine": 5,
        "Cool": 5,
        "Transport": 5,
        "MonsterFarm": 5,
        "Anyone": 5
    }
}
```
