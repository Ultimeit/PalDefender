# 📄 `Pals/ImportRules/*.json`


Reguły importu Palów określają, które pliki `PalTemplate.json` są dozwolone, blokowane lub dostosowywane podczas importowania przez polecenia lub API.

!!! tip "Wyszukiwanie identyfikatorów"
    Identyfikatory do `AllowedPalIDs`, `BannedPalIDs` i nazw plików reguł dla konkretnych Palów znajdziesz na [paldeck.cc/pals](https://paldeck.cc/pals). Do `DisallowedPassives` użyj [paldeck.cc/passives](https://paldeck.cc/passives).

## Położenie plików

| Plik | Przeznaczenie |
| ---- | ------- |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/Default.json` | Globalne reguły importu dla wszystkich szablonów Palów. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/<PalID>.json` | Opcjonalne ustawienia dla konkretnego Pala. Znajdź [`PalID`](https://paldeck.cc/pals) na Paldeck i użyj dokładnie tego ID jako nazwy pliku, np. `Anubis.json`. |
| `<...>/Pal/Binaries/Win64/PalDefender/Pals/ImportRules/ExampleOverride.json` | Automatycznie generowany przykład. Nie jest regułą dla rzeczywistego Pala, dopóki go nie skopiujesz i nie zmienisz nazwy. |

## Klucze

| Klucz | Typ | Opis |
| --- | ---- | ----------- |
| `PalSelectionMode` | ciąg znaków | Tylko w `Default.json`. `AllowAllExceptBanned` pozwala na wszystkie Pale poza `BannedPalIDs`. `AllowOnlyListed` pozwala tylko na `AllowedPalIDs`. |
| `AllowedPalIDs` | tablica | Tylko w `Default.json`. Dozwolone [`PalID`](https://paldeck.cc/pals), gdy `PalSelectionMode` wynosi `AllowOnlyListed`. |
| `BannedPalIDs` | tablica | Tylko w `Default.json`. Identyfikatory [`PalID`](https://paldeck.cc/pals), które są zawsze odrzucane. |
| `MaxValueLimitAction` | ciąg znaków | `BlockImport` odrzuca szablony przekraczające limity. `ClampToMaxValues` obniża wartości do skonfigurowanych limitów. |
| `DisallowedPassivesAction` | ciąg znaków | `BlockImport` odrzuca szablony ze wskazanymi cechami pasywnymi. `RemoveFromPal` usuwa te cechy przed importem. |
| `DisallowedPassives` | tablica | Identyfikatory [`PassiveID`](https://paldeck.cc/passives) objęte działaniem `DisallowedPassivesAction`. |
| `ConditionMode` | ciąg znaków | `None` stosuje regułę bez dodatkowego warunku. `RequirePalCaptureCount` pozwala na import dopiero po schwytaniu przez gracza wymaganej liczby Palów tego samego gatunku. |
| `RequiredCaptureCount` | liczba całkowita | Wymagana liczba schwytanych Palów tego samego gatunku, gdy `ConditionMode` wynosi `RequirePalCaptureCount` (domyślnie `5`). |
| `Disabled` | wartość logiczna | Jeśli `true`, wyłącza kontrole importu dla pasującego zestawu reguł. |
| `BanIfPalIsImpossible` | wartość logiczna | Jeśli `true`, PalDefender może nakładać kary za import niemożliwych Palów zgodnie z ustawieniami serwera. |
| `AllowGenderNone` | wartość logiczna | Jeśli `false`, szablony z `Gender: "None"` mogą zostać odrzucone podczas kontroli importu. |
| `MaxLevel` | liczba całkowita | Najwyższy dozwolony poziom Pala w importowanych szablonach. |
| `MaxRank` | liczba całkowita | Najwyższy dozwolony poziom umiejętności partnerskiej w importowanych szablonach. |
| `PalSouls` | obiekt | Maksymalne dozwolone wartości wzmocnień duszami Palów: `Health`, `Attack`, `Defense`, `CraftSpeed`. |
| `IVs` | obiekt | Maksymalne dozwolone wartości indywidualne (IV): `Health`, `AttackMelee`, `AttackShot`, `Defense`. |

## Zasady przygotowania

1. Zacznij od `Default.json`. Ustaw w nim reguły dla całego serwera.
2. Używaj plików dla konkretnych Palów tylko wtedy, gdy potrzebują innych limitów.
3. Nazwy tych plików muszą odpowiadać ID Pala, np. `Anubis.json`.
4. Nie umieszczaj `PalSelectionMode`, `AllowedPalIDs` ani `BannedPalIDs` w plikach poszczególnych Palów. Należą wyłącznie do `Default.json`.
5. Użyj `BlockImport`, jeśli chcesz rygorystycznie egzekwować ograniczenia.
6. Użyj `ClampToMaxValues`, aby przyjmować szablony, ale obniżać wartości przekraczające limit.
7. Użyj `RemoveFromPal`, aby automatycznie usuwać niedozwolone cechy pasywne zamiast odrzucać import.
8. Zachowaj dokładne ID i sprawdź poprawność JSON przed przesłaniem.

## Konfiguracja krok po kroku

1. Otwórz lub utwórz `Pals/ImportRules/Default.json`.
2. Wybierz globalną politykę dotyczącą Palów:
   - Użyj `AllowAllExceptBanned`, jeśli większość Palów jest dozwolona, a chcesz zablokować tylko kilka.
   - Użyj `AllowOnlyListed`, aby ograniczyć import do zatwierdzonej listy.
3. Wybierz sposób egzekwowania ograniczeń:
   - Użyj `BlockImport` na serwerach, które powinny odrzucać nieprawidłowe szablony.
   - Użyj `ClampToMaxValues`, aby przyjmować szablony, ale obniżać przekroczone poziomy, rangi, wzmocnienia duszami lub IV.
   - Użyj `RemoveFromPal`, aby usuwać niepożądane cechy pasywne zamiast odrzucać cały szablon.
4. Dodaj niedozwolone cechy pasywne z [paldeck.cc/passives](https://paldeck.cc/passives).
5. Dodaj zablokowane lub dozwolone Pale z [paldeck.cc/pals](https://paldeck.cc/pals).
6. Dodaj wyjątek dla konkretnego Pala tylko wtedy, gdy wymaga ostrzejszych lub łagodniejszych limitów niż globalne.
7. Przed importowaniem rozbudowanych szablonów przetestuj prosty `PalTemplate.json`.

## Typowe konfiguracje

### Zezwól na większość Palów, zablokuj wybrane

Użyj tej konfiguracji, jeśli zwykłe nagrody administratora są dozwolone, ale niektórych Palów nie można importować.

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "BannedPalIDs": [
        "JetDragon",
        "BOSS_Anubis"
    ],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

### Zezwól tylko na zatwierdzoną listę

Użyj tej konfiguracji, aby ograniczyć szablony importowane przez graczy do zatwierdzonych Palów.

```json
{
    "PalSelectionMode": "AllowOnlyListed",
    "AllowedPalIDs": [
        "Anubis",
        "Kirin",
        "WeaselDragon"
    ],
    "BannedPalIDs": [],
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "AllowGenderNone": false,
    "MaxLevel": 50,
    "MaxRank": 4,
    "PalSouls": {
        "Health": 10,
        "Attack": 10,
        "Defense": 10,
        "CraftSpeed": 10
    },
    "IVs": {
        "Health": 80,
        "AttackMelee": 80,
        "AttackShot": 80,
        "Defense": 80
    }
}
```

W tej konfiguracji można importować tylko trzy wymienione `PalID`. Wartości przekraczające limity są obniżane do ustawionych maksimów, a wskazane cechy pasywne są usuwane.

## Przykład ustawień domyślnych

```json
{
    "PalSelectionMode": "AllowAllExceptBanned",
    "AllowedPalIDs": [],
    "MaxValueLimitAction": "BlockImport",
    "DisallowedPassivesAction": "BlockImport",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "None",
    "RequiredCaptureCount": 5,
    "Disabled": false,
    "BanIfPalIsImpossible": false,
    "BannedPalIDs": [
        "JetDragon"
    ],
    "AllowGenderNone": false,
    "MaxLevel": 65,
    "MaxRank": 5,
    "PalSouls": {
        "Health": 20,
        "Attack": 20,
        "Defense": 20,
        "CraftSpeed": 20
    },
    "IVs": {
        "Health": 100,
        "AttackMelee": 100,
        "AttackShot": 100,
        "Defense": 100
    }
}
```

## Przykład wyjątku dla konkretnego Pala

### `Anubis.json`
```json
{
    "MaxValueLimitAction": "ClampToMaxValues",
    "DisallowedPassivesAction": "RemoveFromPal",
    "DisallowedPassives": [
        "Legend",
        "Vampire"
    ],
    "ConditionMode": "RequirePalCaptureCount",
    "RequiredCaptureCount": 5,
    "AllowGenderNone": false,
    "MaxLevel": 10,
    "MaxRank": 3,
    "PalSouls": {
        "Health": 5,
        "Attack": 5,
        "Defense": 5,
        "CraftSpeed": 5
    },
    "IVs": {
        "Health": 50,
        "AttackMelee": 50,
        "AttackShot": 50,
        "Defense": 50
    }
}
```
