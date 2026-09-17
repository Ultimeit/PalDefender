# 📄 `PalSummon.json`

Plik PalSummon definiuje walkę w stałym miejscu, uruchamianą przez `/summon <filename>`. Zapisz go w `<PalServer>/Pal/Binaries/Win64/PalDefender/Pals/Summons/`, a wskazane szablony PalTemplate w `Pals/Templates/`.

!!! tip "Wyszukiwanie identyfikatorów"
    `PalID` znajdziesz na [paldeck.cc/pals](https://paldeck.cc/pals), cechy pasywne na [paldeck.cc/passives](https://paldeck.cc/passives), a ID umiejętności użytych w szablonie na [paldeck.cc/skills](https://paldeck.cc/skills).

## Klucze walki

| Klucz | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `PalTemplate` | ciąg znaków | Wymagane | Nazwa szablonu w `Pals/Templates/`; można pominąć `.json`. |
| `BossBattleName` | ciąg znaków | ID Pala | Nazwa wyświetlana w ogłoszeniach, logach, webhookach i wynikach obrażeń. |
| `Uncapturable` | wartość logiczna | `false` | Całkowicie uniemożliwia schwytanie przywołanego Pala. |
| `CapturableAtHealthPercent` | liczba | `15` | Jeśli Pal jest możliwy do schwytania, pozwala na to dopiero przy tym lub niższym odsetku HP (`0`–`100`). Ignorowane, gdy `Uncapturable` wynosi `true`. |
| `DisableAI` | wartość logiczna | `false` | Wyłącza zwykłe AI. Niektóre reakcje, np. uniki, mogą nadal występować. |
| `DisableDamageMeter` | wartość logiczna | `false` | Wyłącza pomiar obrażeń, okno wyników i nagrody za miejsca. Zamiast tego nagrodę `Default` otrzymują wszyscy gracze online. |
| `SpawnScale` | liczba | `1.0` | Mnożnik rozmiaru wizualnego/fizycznego; wartości niedodatnie są zastępowane przez `1.0`. |
| `DamageTakenMultiplier` | liczba | `1.0` | Mnożnik otrzymywanych obrażeń; wartości ujemne są zastępowane przez `1.0`. |
| `DamageDealtMultiplier` | liczba | `1.0` | Mnożnik zadawanych obrażeń; wartości ujemne są zastępowane przez `1.0`. |
| `X`, `Y`, `Z` | liczba | Wymagane | Współrzędne mapy. Pobierz je przez `/getpos`. |
| `DisableStatuses` | tablica | Brak | Nazwy efektów statusu do wyłączenia. Nieprawidłowe nazwy są pomijane. [Dozwolone nazwy](#disable-statuses). |
| `Rewards` | obiekt lub tablica | Brak | Opcjonalne [definicje nagród](#damage-meter-and-rewards) za konkretne miejsca i nagrody domyślnej. Zalecana jest postać obiektu. |

Dla zgodności obsługiwane są aliasy `CapturableAt`, `CapturableAtPercent` i `capturable_at`. Można też użyć `AdditionalEnemyReceiveDamageRate` i `AdditionalEnemyInflictDamageRate`, ale zalecamy nazwy z tabeli.

!!! warning "Zmiana ustawiania maksymalnego HP"
    Maksymalne HP przywołanego Pala pochodzi teraz z pola `HP` wskazanego PalTemplate. `HealthMultiplier`, `HPMultiplier` i `AdditionalEnemyMaxHPRate` nie są już obsługiwane; usuń je z istniejących plików PalSummon.

## Wyłączanie efektów statusu { #disable-statuses }

`DisableStatuses` to tablica nazw efektów statusu zapisanych jako ciągi znaków. Wymienione efekty są usuwane z przywołanego Pala i nie można ich ponownie na niego nałożyć. Wielkość liter nie ma znaczenia; zachowaj angielskie identyfikatory wraz z podkreśleniami. Pusta tablica `[]` nie wyłącza żadnych efektów. Puste ciągi znaków i nieprawidłowe nazwy są pomijane; `None` nie jest dozwolonym wpisem.

Przykład: zablokowanie zatrucia, podpalenia, zamrożenia, efektów elektrycznych, ogłuszenia i snu.

```json
"DisableStatuses": ["Poison", "Burn", "Freeze", "Electrical", "Stun", "Sleep"]
```

Pełna lista obejmuje również wzmocnienia i wewnętrzne stany gry, a nie tylko szkodliwe efekty.

??? info "Wszystkie dozwolone nazwy efektów statusu"
    --8<-- "_snippets/pals/disable-statuses.md"


## Pomiar obrażeń i nagrody { #damage-meter-and-rewards }

Nagrody są ustalane po śmierci lub schwytaniu przywołanego Pala. Ranking jest sortowany od największych do najmniejszych obrażeń. Okno wyników pokazuje pierwszą piątkę, wyróżnia pierwszą trójkę i podaje także miejsce odbiorcy, jeśli jest on poza pierwszą piątką.

Przy włączonym pomiarze obrażeń każdy uczestnik jest obsługiwany następująco:

1. PalDefender szuka liczbowego klucza `Rewards` odpowiadającego końcowemu miejscu gracza.
2. Jeśli takiego miejsca nie zdefiniowano, używa `Rewards.Default`.
3. Jeśli nie ma żadnej z tych definicji, gracz nie dostaje nagrody.
4. Wybrana nagroda jest losowana osobno dla gracza. Dwaj gracze korzystający z tej samej definicji `Default` mogą otrzymać inne wyniki.

Nagrody za miejsca otrzymują tylko uczestnicy, którzy w chwili zakończenia walki nadal są online i mają dostępny kontroler gracza. Nagroda z kluczem liczbowym zastępuje `Default` dla danego miejsca, a nie dodaje się do niej.

```json
"Rewards": {
    "1": {
        "Drops": [
            { "ItemID": "Money", "Count": 50000 },
            { "TechnologyPoints": 5 }
        ]
    },
    "2": {
        "Drops": [
            { "EXP": { "Min": 10000, "Max": 20000 } }
        ]
    },
    "Default": {
        "Drops": [
            { "ItemID": "Money", "Count": 1000, "Chance": 75 }
        ]
    }
}
```

W tym przykładzie pierwsze miejsce otrzymuje obie gwarantowane nagrody, drugie — losową ilość EXP, a każdy pozostały uczestnik rankingu ma niezależną szansę 75% na 1000 jednostek `Money`.

Klucze miejsc muszą być dodatnimi liczbami całkowitymi zapisanymi jako klucze obiektu JSON, np. `"1"`, `"2"` lub `"10"`. `"0"`, miejsca ujemne i dowolne nazwy są nieprawidłowe. Dla `Default` wielkość liter nie ma znaczenia.

??? note "Postać tablicy"
    `Rewards` może też być tablicą. Element o indeksie 0 odpowiada miejscu 1, indeks 1 — miejscu 2 itd. Tablica nie pozwala zdefiniować `Default`, dlatego zalecamy czytelniejszą postać obiektu.

    ```json
    "Rewards": [
        { "Drops": [ { "ItemID": "Money", "Count": 50000 } ] },
        { "Drops": [ { "ItemID": "Money", "Count": 25000 } ] }
    ]
    ```

### Struktura definicji nagrody

Każde miejsce i `Default` zawiera jedną definicję nagrody. Może ona obejmować oba pola:

- `Drops`: wpisy oceniane bezpośrednio i niezależnie.
- `Pools`: grupy określające sposób wybierania wpisów.

Może też zawierać skrótowe pola postępów: `EXP`, `TechnologyPoints` i `AncientTechnologyPoints`. Ich przyznanie jest gwarantowane. Są przydatne, gdy nie wymagają osobnych ustawień `Chance`, `Weight` ani `Unique`.

```json
{
    "EXP": { "Min": 10000, "Max": 20000 },
    "TechnologyPoints": 2,
    "AncientTechnologyPoints": 1,
    "Drops": [
        { "ItemID": "Money", "Count": 5000 }
    ],
    "Pools": [
        {
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

### Rodzaje wpisów nagród

Każdy wpis musi określać dokładnie jeden rodzaj nagrody. Nie łącz przedmiotu, jaja i pola postępów w jednym wpisie.

| Nagroda | Pola wymagane | Pola opcjonalne | Uwagi |
| --- | --- | --- | --- |
| Przedmiot | `ItemID` | `Count`, `Chance`, `Weight`, `Unique` | `Count` domyślnie wynosi `1`. |
| Jajo Pala | `EggID`, `PalTemplate` | `Count`, `Level`, `Chance`, `Weight`, `Unique` | `Count` domyślnie wynosi `1`; `Level: 0` używa poziomu z szablonu. |
| Doświadczenie | `EXP` | `Chance`, `Weight`, `Unique` | Wartość `EXP` to ilość lub zakres. |
| Punkty technologii | `TechnologyPoints` | `Chance`, `Weight`, `Unique` | Wartość pola to ilość lub zakres. |
| Punkty starożytnej technologii | `AncientTechnologyPoints` | `Chance`, `Weight`, `Unique` | Wartość pola to ilość lub zakres. |

`Chance`, `Weight` i `Unique` działają tylko w opisanych niżej sytuacjach. Akceptacja pola przez parser nie oznacza, że wpływa ono na każdy tryb przyznawania nagród.

Zalecamy powyższe nazwy podstawowe. Parser akceptuje również następujące aliasy:

| Nazwa podstawowa | Obsługiwane aliasy |
| --- | --- |
| `ItemID` | `ItemId`, `ID` |
| `EggID` | `EggId` |
| `PalTemplate` | `Template` |
| `Count` | `Amount`, `Num` |
| `EXP` | `Exp`, `Experience` |
| `TechnologyPoints` | `TechPoints` |
| `AncientTechnologyPoints` | `BossTechnologyPoints` |

### Stałe wartości, zakresy i prawdopodobieństwo

Ilości mogą być stałą liczbą całkowitą lub zakresem obejmującym obie granice:

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 25000 },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
        { "EXP": { "Min": 10000, "Max": 20000 } },
        { "TechnologyPoints": 2 }
    ]
}
```

- `Count`, EXP i ilości punktów technologii muszą być liczbami całkowitymi co najmniej `1`.
- Zakres wymaga `Min` i `Max`; `Max` nie może być mniejsze od `Min`.
- Zakresy tekstowe, np. `"1-3"`, są nieprawidłowe. Użyj `{ "Min": 1, "Max": 3 }`.
- `Level` jaja może wynosić `0`, co zachowuje poziom z PalTemplate. Wartość dodatnia zastępuje poziom szablonu i jest ograniczana do 255 przy przyznawaniu jaja.
- `Chance` przyjmuje liczbę lub tekst liczbowy z opcjonalnym `%`, np. `30`, `30.5` lub `"30%"`.
- `Chance: 0` nigdy nie daje nagrody, a `Chance: 100` zawsze ją daje. Wartości muszą mieścić się między `0` a `100`.
- Przy szansie większej od 0 i mniejszej od 100 wylosowana liczba musi być mniejsza od ustawionej wartości. Wynik dokładnie `30.0` nie daje więc nagrody przy `Chance: 30`.

### Nagrody bezpośrednie

Każdy wpis w `Drops` jest oceniany niezależnie. Sąsiednie wpisy nie konkurują o wybór jednej nagrody. Brak `Chance` oznacza `100`.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": { "Min": 25000, "Max": 75000 } },
        { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 }, "Chance": 30 },
        { "EXP": 15000, "Chance": "50%" },
        { "TechnologyPoints": 2, "Chance": 10 }
    ]
}
```

`Money` jest gwarantowane. Amunicja, EXP i punkty technologii są losowane osobno. Można otrzymać zero, jedną, dwie lub wszystkie trzy opcjonalne nagrody.

`Weight` i `Unique` nie działają w bezpośrednich `Drops` i powodują ostrzeżenia. Do opcjonalnych nagród bezpośrednich użyj `Chance`.

## Pule nagród

Najpierw losowana jest szansa `Chance` całej puli. Jeśli losowanie się nie powiedzie, żaden wpis nie jest rozpatrywany. Jeśli się powiedzie, `Mode` określa sposób oceny wpisów.

| Klucz puli | Typ | Wartość domyślna | Opis |
| --- | --- | --- | --- |
| `Name` | ciąg znaków | Brak | Opcjonalna nazwa diagnostyczna. Nie wpływa na wybór. |
| `Mode` | ciąg znaków | `OneOf` | `OneOf`, `Pick`, `All` lub `Independent`. Wielkość liter nie ma znaczenia. |
| `Chance` | liczba lub tekst procentowy | `100` | Szansa aktywacji całej puli. |
| `Rolls` | liczba całkowita | `1` | Liczba losowań w `Pick`; ignorowana w innych trybach. |
| `Unique` | wartość logiczna | `true` | Domyślna zasada powtórzeń w `Pick`; wpis może ją nadpisać. |
| `Entries` | tablica | Wymagane | Niepusta lista wpisów nagród. |

`One` jest aliasem `OneOf`, a `PickN` aliasem `Pick`, ale zalecamy nazwy podstawowe.

| Tryb | Ile wpisów można przyznać? | Używa `Weight`? | Używa `Chance` wpisu? | Używa `Rolls` / `Unique`? |
| --- | --- | --- | --- | --- |
| `OneOf` | Dokładnie jeden po aktywacji puli | Tak | Nie | No |
| `Pick` | Do `Rolls` losowań | Tak | Nie | Tak |
| `All` | Każdy wpis raz po aktywacji puli | Nie | No | Nie |
| `Independent` | Od zera do wszystkich wpisów | Nie | Tak | Nie |

Wszystkie cztery tryby używają `Chance` całej puli. Pule w jednej definicji są przetwarzane niezależnie, a ich wyniki dodawane do bezpośrednich `Drops`.

### `OneOf`: jeden wynik wybierany według wag

`OneOf` jest trybem domyślnym. Po aktywacji puli wybiera dokładnie jeden wpis. Szansa wpisu to jego `Weight` podzielone przez sumę wag wszystkich wpisów.

```json
{
    "Pools": [
        {
            "Name": "Główna nagroda wyposażenia",
            "Mode": "OneOf",
            "Chance": 35,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 7 },
                { "ItemID": "AncientHelmet", "Weight": 7 },
                { "ItemID": "SkyAssaultRifle", "Weight": 5 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Weight": 1 }
            ]
        }
    ]
}
```

Suma wag wynosi 20. Po aktywacji puli szanse czterech wpisów wynoszą 35%, 35%, 25% i 5%. Ponieważ sama pula aktywuje się z szansą 35%, całkowita szansa na jajo to `35% × 5% = 1.75%`.

- Brak `Weight` oznacza `1`.
- `Weight` musi być liczbą całkowitą co najmniej `1`. Zamiast ustawiać wagę `0`, usuń wpis.
- `Rolls` jest ignorowane i powoduje ostrzeżenie, ponieważ `OneOf` zawsze wybiera jeden raz.
- `Chance` wpisu jest ignorowane i powoduje ostrzeżenie. Względne prawdopodobieństwo wyboru ustaw przez `Weight`.
- `Unique` nie ma praktycznego znaczenia, bo wybierany jest tylko jeden wpis.

### `Pick`: wiele wyników według wag, bez powtórzeń

`Pick` powtarza wybór według wag `Rolls` razy. Przy domyślnym `Unique: true` wybrany wpis jest usuwany przed następnym losowaniem i nie może wypaść ponownie. Po każdym wyborze wagi są przeliczane dla pozostałych wpisów.

```json
{
    "Pools": [
        {
            "Name": "Dwie różne nagrody",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": true,
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 },
                { "ItemID": "SkyAssaultRifle", "Weight": 1 }
            ]
        }
    ]
}
```

Przyznaje to dwa różne wpisy. Jeśli `Rolls` przekracza liczbę dostępnych unikalnych wpisów, losowanie kończy się po ich wyczerpaniu. Nie jest to błąd.

### `Pick`: dopuszczanie powtórzeń

Ustaw `Unique` puli na `false`, aby wybrane wpisy pozostały dostępne w kolejnych losowaniach. Powtarzające się nagrody tego samego przedmiotu są łączone przed przyznaniem.

```json
{
    "Pools": [
        {
            "Name": "Trzy losowania zaopatrzenia",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 5 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 2 }
            ]
        }
    ]
}
```

Wszystkie trzy losowania mogą dać `Money`, amunicję lub mieszane wyniki. Przykładowo dwukrotny wybór `Money` daje jedno przyznanie 10 000 jednostek zamiast dwóch osobnych.

### `Pick`: nadpisywanie `Unique` we wpisie

`Unique` wpisu zastępuje ustawienie puli tylko dla tego wpisu. Pozwala to łączyć powtarzalne zwykłe nagrody z wyjątkowymi nagrodami jednorazowymi.

```json
{
    "Pools": [
        {
            "Name": "Powtarzalna waluta i unikalne nagrody główne",
            "Mode": "Pick",
            "Rolls": 3,
            "Unique": true,
            "Entries": [
                { "ItemID": "Money", "Count": { "Min": 5000, "Max": 7000 }, "Weight": 10, "Unique": false },
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        }
    ]
}
```

`Money` pozostaje na liście po wyborze, ponieważ ma `Unique: false`. Pancerz i hełm dziedziczą `Unique: true` z puli i są usuwane po wyborze. Możliwa jest też sytuacja odwrotna: pula ma `Unique: false`, a konkretny wpis `Unique: true`.

### `All`: przyznaj wszystkie wpisy

`All` przyznaje każdy wpis dokładnie raz po udanym losowaniu `Chance` puli.

```json
{
    "Pools": [
        {
            "Name": "Pełny zestaw nagród",
            "Mode": "All",
            "Chance": 100,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": { "Min": 100, "Max": 250 } },
                { "EXP": 15000 },
                { "TechnologyPoints": 2 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": 50 }
            ]
        }
    ]
}
```

`Weight`, `Chance` wpisu i `Unique` nie wpływają na `All`. `Rolls` jest ignorowane i powoduje ostrzeżenie. Aby losować cały zestaw, ustaw `Chance` puli. Aby losować pojedyncze wpisy, użyj `Independent` lub bezpośrednich `Drops`.

### `Independent`: losuj każdy wpis osobno

`Independent` sprawdza każdy wpis według jego własnego `Chance`. Może przyznać zero, jeden, kilka lub wszystkie wpisy.

```json
{
    "Pools": [
        {
            "Name": "Niezależne losowania bonusów",
            "Mode": "Independent",
            "Chance": 80,
            "Entries": [
                { "ItemID": "Money", "Count": 10000 },
                { "ItemID": "AssaultRifleBullet", "Count": 250, "Chance": 50 },
                { "ItemID": "AncientArmor", "Chance": 10 },
                { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Chance": 5 }
            ]
        }
    ]
}
```

Najpierw pula ma 80% szans na aktywację. Po aktywacji `Money` jest gwarantowane, bo jego wpis nie ma `Chance`. Pozostałe trzy wpisy są losowane niezależnie z szansami 50%, 10% i 5%.

- Brak `Chance` wpisu oznacza `100`.
- `Weight` i `Unique` nie wpływają na ten tryb.
- `Rolls` jest ignorowane i powoduje ostrzeżenie, bo każdy wpis jest sprawdzany raz.

### Łączenie nagród bezpośrednich i wielu pul

Użyj wielu pul, jeśli odbiorca ma otrzymać kilka niezależnie skonfigurowanych grup nagród.

```json
{
    "Drops": [
        { "ItemID": "Money", "Count": 10000 },
        { "EXP": 5000 }
    ],
    "Pools": [
        {
            "Name": "Jeden element wyposażenia",
            "Mode": "OneOf",
            "Entries": [
                { "ItemID": "AncientArmor", "Weight": 1 },
                { "ItemID": "AncientHelmet", "Weight": 1 }
            ]
        },
        {
            "Name": "Dwa losowania zaopatrzenia",
            "Mode": "Pick",
            "Rolls": 2,
            "Unique": false,
            "Entries": [
                { "ItemID": "Money", "Count": 5000, "Weight": 3 },
                { "ItemID": "AssaultRifleBullet", "Count": 100, "Weight": 1 }
            ]
        },
        {
            "Name": "Rzadkie niezależne bonusy",
            "Mode": "Independent",
            "Entries": [
                { "TechnologyPoints": 1, "Chance": 20 },
                { "AncientTechnologyPoints": 1, "Chance": 5 }
            ]
        }
    ]
}
```

Bezpośrednie `Money` i EXP są zawsze przyznawane. Pierwsza pula dodaje jeden element wyposażenia, druga losuje dwa razy zaopatrzenie według wag z powtórzeniami, a trzecia wykonuje dwa niezależne losowania bonusów. Gracz może otrzymać wyniki ze wszystkich pul, bo pule nie konkurują ze sobą.

### Nagrody w postaci jaj Palów

Jajo wymaga `EggID` i `PalTemplate`. Szablon jest wczytywany z `Pals/Templates/`; można pominąć `.json`. `Count` określa liczbę jaj. `Level: 0` lub brak poziomu zachowuje poziom szablonu; dodatnia wartość stała lub zakres go zastępuje.

```json
{
    "Pools": [
        {
            "Name": "Jedna losowa nagroda w postaci jaja",
            "Mode": "OneOf",
            "Entries": [
                {
                    "EggID": "PalEgg_Dark_05",
                    "PalTemplate": "RaidReward.json",
                    "Count": 1,
                    "Level": { "Min": 45, "Max": 55 },
                    "Weight": 3
                },
                {
                    "EggID": "PalEgg_Dragon_05",
                    "PalTemplate": "DragonReward.json",
                    "Count": { "Min": 1, "Max": 2 },
                    "Level": 50,
                    "Weight": 1
                }
            ]
        }
    ]
}
```

Jeśli podczas przyznawania nagrody nie można zaimportować szablonu jaja, PalDefender zapisuje błąd i pomija tę nagrodę.

### Łączenie powtarzających się wyników

Wyniki nagród bezpośrednich i wszystkich pul są łączone przed przyznaniem:

- Przedmioty z tym samym `ItemID` są łączone przez sumowanie ilości.
- Jaja są łączone tylko wtedy, gdy `EggID`, `PalTemplate` i wylosowany `Level` są identyczne.
- EXP, punkty technologii i punkty starożytnej technologii są sumowane oddzielnie.
- Łączne ilości przedmiotów i punktów technologii są ograniczane do maksimum 32-bitowej liczby całkowitej ze znakiem (`2,147,483,647`).

Powtarzające się wyniki `Pick` nie tworzą więc zduplikowanych pozycji ekwipunku w żądaniu nagrody. Jaja o różnych wylosowanych poziomach pozostają osobnymi nagrodami.

### Przyznawanie nagród przy `DisableDamageMeter`

Gdy `DisableDamageMeter` wynosi `true`, PalDefender nie tworzy rankingu obrażeń ani nie używa nagród za miejsca. Zamiast tego losuje `Rewards.Default` osobno dla **każdego gracza online w chwili zakończenia walki**, także tych, którzy nie zadali obrażeń przywołanemu Palowi.

```json
{
    "DisableDamageMeter": true,
    "Rewards": {
        "Default": {
            "Drops": [
                { "ItemID": "Money", "Count": 5000 }
            ],
            "Pools": [
                {
                    "Mode": "Independent",
                    "Entries": [
                        { "TechnologyPoints": 1, "Chance": 25 },
                        { "AncientTechnologyPoints": 1, "Chance": 5 }
                    ]
                }
            ]
        }
    }
}
```

Każdy gracz online otrzymuje `Money`. Dwie opcjonalne nagrody punktowe są losowane osobno dla każdego gracza. Jeśli `Default` nie istnieje lub jest puste, nikt nie dostaje nagrody w tym trybie, a PalDefender zapisuje ostrzeżenie.

### Nieprawidłowe i ignorowane kombinacje

Nieprawidłowe dane nagród uniemożliwiają wczytanie PalSummon. Nieznane lub ignorowane w danym kontekście pola powodują ostrzeżenia, dzięki czemu literówki i nieskuteczne ustawienia są widoczne w logu PalDefender.

| Konfiguracja | Wynik |
| --- | --- |
| Jeden wpis zawiera `ItemID` i `EXP` | Błąd: wpis może określać tylko jeden rodzaj nagrody. |
| Wpis nie zawiera pola przedmiotu, jaja ani postępów | Błąd: PalDefender nie wie, co przyznać. |
| `Count: 0`, `Weight: 0` lub `Rolls: 0` | Błąd: wartości muszą wynosić co najmniej `1`. |
| Zakres nie zawiera `Min` lub `Max` albo ma `Max < Min` | Błąd. |
| `Chance` jest poza zakresem `0`–`100` | Błąd. |
| Pula nie ma `Entries`, ma pustą tablicę `Entries` lub wartość niebędącą tablicą | Błąd. |
| `Chance` jest ustawione we wpisie `OneOf`, `Pick` lub `All` | Ostrzeżenie; szansa wpisu jest ignorowana. |
| `Rolls` jest ustawione w `OneOf`, `All` lub `Independent` | Ostrzeżenie; `Rolls` jest ignorowane. |
| `Weight` lub `Unique` jest ustawione w bezpośrednich `Drops` | Ostrzeżenie; użyj `Chance` do nagród bezpośrednich. |
| Występuje nieznane pole, np. `Wieght` | Ostrzeżenie; pole nie jest używane. |

Używaj poprawnego JSON bez komentarzy i przecinków po ostatnich elementach. Sprawdzaj ostrzeżenia nawet po udanym wczytaniu przywołania: zwykle wskazują ustawienie, które nie działa.

## Pełny przykład

```json
{
    "PalTemplate": "ArenaBoss.json",
    "BossBattleName": "Anubis z areny",
    "Uncapturable": false,
    "CapturableAtHealthPercent": 10,
    "DisableAI": false,
    "DisableDamageMeter": false,
    "SpawnScale": 1.5,
    "DamageTakenMultiplier": 0.75,
    "DamageDealtMultiplier": 2.0,
    "X": 230,
    "Y": -486,
    "Z": 4097,
    "DisableStatuses": ["Poison", "Burn", "Freeze"],
    "Rewards": {
        "1": {
            "Drops": [
                { "ItemID": "Money", "Count": 50000 },
                { "AncientTechnologyPoints": 3 }
            ],
            "Pools": [
                {
                    "Name": "Bonus zwycięzcy",
                    "Mode": "Pick",
                    "Rolls": 2,
                    "Unique": true,
                    "Entries": [
                        { "ItemID": "AncientCivilizationParts", "Count": { "Min": 1, "Max": 3 }, "Weight": 5 },
                        { "EggID": "PalEgg_Dark_05", "PalTemplate": "RaidReward.json", "Level": { "Min": 45, "Max": 55 }, "Weight": 1 }
                    ]
                }
            ]
        },
        "Default": {
            "Drops": [
                { "EXP": 5000 },
                { "TechnologyPoints": 1 }
            ]
        }
    }
}
```

## Lista kontrolna

1. Najpierw przetestuj szablon przez `/givemepal_j <template>`.
2. Pobierz `X`, `Y` i `Z` przez `/getpos`; RCON musi podać UserId w `/getpos`.
3. Używaj poprawnego JSON bez komentarzy i przecinków po ostatnich elementach.
4. Używaj tylko jednego rodzaju nagrody w każdym wpisie.
5. Sprawdź, czy każda pula ma niepuste `Entries` i używa tylko pól działających w wybranym `Mode`.
6. Uruchom `/summon <filename>` i sprawdź log PalDefender pod kątem szczegółowych błędów weryfikacji i ostrzeżeń.
