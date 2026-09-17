# POST `/v1/pdapi/give`

<span class='pd-badge pd-badge--deprecated'>Przestarzałe</span>

!!! warning "<span class='pd-badge pd-badge--deprecated'>Przestarzałe</span> — starszy punkt końcowy"
    Ten starszy punkt końcowy przyznawania nagród jest przestarzały. Korzystaj z osobnych punktów końcowych: [przyznawanie postępów](./give-progression.md), [przedmiotów](./give-items.md), [Pali](./give-pals.md), [szablonów Pali](./give-paltemplate.md) i [jaj Pali](./give-paleggs.md).


## Schemat odpowiedzi

--8<-- "_snippets/pl/restapi/schemas/give_deprecated.md"

## Odpowiedzi błędów

Ten punkt końcowy jest przestarzały i może być niedostępny w obecnych kompilacjach. Jeśli jest dostępny, odpowiedzi błędów mają taki sam format REST jak w aktualnym API.

| HTTP | Kod błędu | Kiedy występuje |
|------|------------|-----------------|
| `401` | `INVALID_TOKEN` | Brakuje nagłówka `Authorization`, ma on nieprawidłowy format lub nie odpowiada żadnemu skonfigurowanemu tokenowi Bearer. |
| `403` | `MISSING_PERMISSION` | Token jest prawidłowy, ale nie ma uprawnienia do tej przestarzałej ścieżki. |
| `400` | `INVALID_JSON` | Przesłano treść żądania, ale nie można jej odczytać jako JSON. |
| `400` | `REQUEST_FAILED` | Starsza operacja przyznawania nagród nie powiodła się podczas walidacji lub wykonywania żądania. |
| `500` | `REQUEST_TIMEOUT` | Wewnętrzna funkcja wywołana w wątku gry nie zakończyła się w ciągu 5 sekund. |

## Przykłady

### Przyznanie EXP i przedmiotów

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "steam_76561198012345678",
    "EXP": 25000,
    "Items": [
        { "ItemID": "Money", "Count": 10000 }
    ]
}
```

### Przyznanie Pali i jaj

```http
POST /v1/pdapi/give
```

```json
{
    "UserID": "ps5_0f4b8c2d91aa34ef",
    "Pals": [
        { "PalID": "Pengullet", "Level": 10 }
    ],
    "PalEggs": [
        { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
    ]
}
```

??? info "POST `/v1/pdapi/give` — Przyznawanie EXP / przedmiotów / Pali / jaj (atomowo)"
    ## POST `/v1/pdapi/give`
    ### Działanie
    Przyznaje wskazanemu graczowi nagrody w jednej operacji po stronie serwera, działającej podobnie do transakcji:

    - EXP i/lub
    - przedmioty i/lub
    - Pale i/lub
    - jaja
    zależnie od treści żądania.

    ### Podstawowe zasady
    Ten punkt końcowy powinien działać **atomowo**:

    - albo przyznaje wszystkie nagrody
    - albo nie przyznaje żadnej

    Jeśli dowolny etap zawiedzie (nieprawidłowe dane, brak miejsca w ekwipunku, błędne identyfikatory itp.), serwer powinien odrzucić całe żądanie i nie wykonywać go częściowo.

    ### Dlaczego to ma znaczenie
    Narzędzia administratora nie powinny przypadkowo:

    - przyznawać EXP bez przedmiotów
    - przyznawać części przedmiotów i zawodzić przy kolejnych
    - tworzyć Pali bez przekazania przedmiotów

    Atomowe działanie zapobiega niespójnym stanom i wyjątkowo trudnym zgłoszeniom do pomocy technicznej.

    ### Dostępne nagrody
    W zależności od implementacji żądanie może zawierać:

    - `EXP` — dodaje doświadczenie
    - `Relics` — dodaje punkty reliktów według typu reliktu
    - `TechnologyPoints` — dodaje punkty technologii
    - `AncientTechnologyPoints` — dodaje punkty starożytnej technologii
    - `UnlockTechnology` / `Techs[]` — odblokowuje technologie
    - `Items[]` — przyznaje przedmioty w określonych liczbach
    - `Pals[]` — przyznaje Pale według identyfikatora i poziomu
    - `PalTemplates[]` — importuje szablony Pali według nazwy pliku
    - `PalEggs[]` — przyznaje jaja według identyfikatora jaja i identyfikatora Pala lub szablonu, opcjonalnie z poziomem


    ### Odpowiedzi błędów

    Ten punkt końcowy jest przestarzały i może być niedostępny w obecnych kompilacjach. Jeśli jest dostępny, używa tego samego formatu błędów REST co aktualne API: `INVALID_TOKEN` (`401`) oznacza nieudane uwierzytelnianie tokenem Bearer, a `MISSING_PERMISSION` (`403`) — prawidłowy token bez uprawnień do tej ścieżki. Błędy walidacji żądania są zwracane jako obiekty JSON. Przejdź na osobne punkty końcowe nagród, aby otrzymywać właściwe dla nich kody błędów.

    ### Przykłady

    ```json
    {
        "UserID": "steam_76561198012345678",
        "EXP": 25000,
        "Items": [
            { "ItemID": "Money", "Count": 10000 }
        ]
    }
    ```

    ```json
    {
        "UserID": "steam_76561198012345678",
        "Pals": [
            { "PalID": "Pengullet", "Level": 10 }
        ],
        "PalEggs": [
            { "EggID": "PalEgg_Fire_01", "PalID": "Foxparks", "Level": 12 }
        ]
    }
    ```

    ### Walidacja i typowe przyczyny błędów
    Typowe przyczyny błędów:

    - Miejsce w ekwipunku: brak miejsca na wszystkie przedmioty → odrzucenie całego żądania
    - Błędne identyfikatory: nieznane `ItemID`, `PalID`, `EggID` lub brak pliku szablonu → odrzucenie
    - Nieprawidłowe wartości:
        - ujemna lub zerowa liczba sztuk (zależnie od zasad)
        - błędne poziomy (zbyt niskie/wysokie lub nieliczbowe)
        - brak wymaganych pól (np. `UserID`)
    - Nie znaleziono lub nie wczytano gracza:
        - nieznany identyfikator użytkownika
        - gracz nie jest online (zależnie od obsługi przyznawania nagród offline na serwerze)

    ### Zwracane dane
    Liczba błędów i ich komunikaty. Jeśli kod odpowiedzi jest inny niż 200, pole `Errors` zawiera liczbę błędów. `Error` zawiera szczegółową listę niepowodzeń.
