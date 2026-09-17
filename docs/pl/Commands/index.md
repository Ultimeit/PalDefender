# Polecenia

## Czym są polecenia?

Polecenia to specjalne instrukcje tekstowe służące do wykonywania działań w grze. Wpisując je na czacie, możesz między innymi teleportować się, tworzyć stworzenia i zarządzać graczami. Polecenia zwykle zaczynają się od znaku <span class="var-command">/</span>, po którym podaje się nazwę polecenia i ewentualne argumenty.

## Kto może używać poleceń?

**Obecnie żadne polecenie nie jest dostępne dla graczy bez uprawnień administratora.**
W obecnej wersji dostępne są wyłącznie polecenia administratora i RCON.

## Lista poleceń

!!! note "Składnia poleceń"
    <span class="var-command">/nazwa_polecenia&nbsp;</span><span class="var-command-arg">&lt;argument_wymagany&gt;&nbsp;</span><span class="var-command-optional">[argument_opcjonalny={?}]</span>
    <br>
    <br>
    <p>
    <span class="var-command-arg">&lt;argument_wymagany&gt;</span> → Należy go podać.<br>
    <span class="var-command-optional">[argument_opcjonalny={?}]</span> → Można go pominąć. Symbol <span class="var-command-optional">{?}</span> oznacza wartość domyślną stosowaną po pominięciu argumentu.
    </p>
    <p>
    Argumenty mogą mieć różne typy. Najczęściej są to <span class="var-string">ciągi znaków</span>, <span class="var-number">liczby</span>, <span class="var-float">liczby zmiennoprzecinkowe</span> i <span class="var-bool">wartości logiczne</span>. Niektóre polecenia przyjmują także bardziej złożone argumenty, na przykład <span class="file">nazwy plików</span> w określonym katalogu lub <span class="var-filter">filtr</span>.
    </p>

!!! tip "Wyszukiwanie identyfikatorów"
    Identyfikatory znajdziesz na stronach: [paldeck.cc/pals](https://paldeck.cc/pals) — `PalID`, [paldeck.cc/items](https://paldeck.cc/items) — `ItemID`, [paldeck.cc/technology](https://paldeck.cc/technology) — `TechID`, [paldeck.cc/buildings](https://paldeck.cc/buildings) — `BuildingID`, [paldeck.cc/passives](https://paldeck.cc/passives) — `PassiveID` oraz [paldeck.cc/skills](https://paldeck.cc/skills) — identyfikatory umiejętności.

??? note "Tylko RCON"
    ??? info "/getrconcmds"
        **Składnia:** `/getrconcmds`

        **Opis:** Zwraca listę wszystkich poleceń dostępnych przez RCON wraz z liczbą wymaganych argumentów.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `RCON`

        **Przykład:**
        ```
        /getrconcmds
        ```

??? note "Zarządzanie serwerem"
    ??? info "/version"
        **Składnia:** `/version`

        **Opis:** Wyświetla wersję gry Palworld i wersję PalDefender. RCON zwraca wynik w formacie JSON.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /version
        ```

    ??? info "/reloadcfg"
        **Składnia:** `/reloadcfg`

        **Opis:** Ponownie wczytuje `Config.json`, `WhiteList.json` oraz dane blokad PalDefender.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /reloadcfg
        ```

    ??? info "/addadminip"
        **Składnia:** `/addadminip <IP>`

        **Opis:** Dodaje adres IP do listy dozwolonych adresów administratorów.

        **Argumenty:**

        - `<IP>`: Adres IP do dodania do listy administratorów.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /addadminip 192.168.1.1
        ```

    ??? info "/setadmin"
        **Składnia:** `/setadmin <UserId>`

        **Opis:** Tymczasowo nadaje lub odbiera graczowi uprawnienia administratora.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza, któremu należy nadać lub odebrać uprawnienia administratora.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /setadmin steam_76500000000000000
        ```

    ??? info "/pgbroadcast"
        **Składnia:** `/pgbroadcast <Message>`

        **Opis:** Wysyła wiadomość do wszystkich graczy na serwerze.

        **Argumenty:**

        - `<Message>`: Treść wiadomości do wysłania wszystkim graczom.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /pgbroadcast "Serwer wkrótce zostanie uruchomiony ponownie."
        ```

    ??? info "/adminlogin"
        **Składnia:** `/adminlogin <password>`

        **Opis:** Włącza tryb administratora. Jako argument należy podać hasło administratora.

        **Argumenty:**

        - `<password>`: Hasło administratora.

        **Uprawnienia:** `Chat`

        **Przykład:**
        ```
        /adminlogin mojeTajneHaslo
        ```

    ??? info "/adminlogout"
        **Składnia:** `/adminlogout`

        **Opis:** Wyłącza tryb administratora.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /adminlogout
        ```

    ??? info "/iwantplayerlist"
        **Składnia:** `/iwantplayerlist`

        **Opis:** Włącza nakładkę z listą graczy w grze. Po naciśnięciu ESC wyświetlane są identyfikatory UserId i Player UID każdego gracza. Przydaje się administratorom i graczom, którzy chcą sprawdzać szczegółowe informacje o graczach bezpośrednio w interfejsie gry.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /iwantplayerlist
        ```

    ??? info "/getpos"
        **Składnia:** `/getpos [UserId]`

        **Opis:** Odczytuje twoją bieżącą pozycję w świecie, przydatną przy teleportowaniu, przywoływaniu i podobnych działaniach. Jeśli podasz [UserId], odczyta pozycję wskazanego gracza.

        **Argumenty:**

        - `[UserId]`: (Opcjonalnie) Identyfikator gracza, którego pozycję chcesz odczytać. Pominięcie powoduje odczyt twojej pozycji.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /getpos
        /getpos steam_76500000000000000
        ```

    ??? info "/settime"
        **Składnia:** `/settime <hour>`

        **Opis:** Zmienia czas w Palworld. Dozwolone wartości godziny to liczby od `0` do `23` oraz `day` i `night`.

        **Argumenty:**

        - `<hour>`: Godzina (0–23, day, night).

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /settime 12
        /settime night
        ```

    ??? info "/togglepvp"
        **Składnia:** `/togglepvp`

        **Opis:** Włącza lub wyłącza PvP na serwerze w bieżącej sesji.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /togglepvp
        ```

    ??? info "/alert"
        **Składnia:** `/alert <message>`

        **Opis:** Wysyła alert do wszystkich graczy na serwerze. Wiadomość zwykle pojawia się w dobrze widocznym miejscu na ekranie.

        **Argumenty:**

        - `<message>`: Treść alertu do wysłania wszystkim graczom.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /alert Serwer zostanie uruchomiony ponownie za 5 minut!
        ```

    ??? info "/send"
        **Składnia:** `/send <type> <UserId> <Message>`

        **Opis:** Wysyła wiadomość na czacie lub komunikat systemowy do wskazanego gracza.

        **Argumenty:**

        - `<type>`: Typ wysyłanej wiadomości. Dostępne wartości:
             - `msg`: Zwykła wiadomość na czacie.
             - `log`: Zwykły komunikat systemowy (biały, szybko znika, większa czcionka).
             - `ilog`: Ważny komunikat systemowy (niebieski, pozostaje dłużej).
             - `vilog`: Bardzo ważny komunikat systemowy (niebieski, pozostaje bardzo długo).
        - `<UserId>`: Identyfikator odbiorcy wiadomości.
        - `<Message>`: Treść wysyłanej wiadomości.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /send msg steam_76500000000000000 Nie przegap promocji Qonzer!
        /send log steam_76500000000000000 Nie przegap promocji Qonzer!
        /send ilog steam_76500000000000000 Nie przegap promocji Qonzer!
        /send vilog steam_76500000000000000 Nie przegap promocji Qonzer!
        ```

    ??? info "/resetoilrig"
        **Składnia:** `/resetoilrig <lv30|lv55|lv60|all>`

        **Opis:** Resetuje wybraną platformę wiertniczą lub wszystkie aktualnie zarządzane platformy.

        **Uprawnienia:** `Chat`, aktywny status administratora w grze.

        **Przykład:**
        ```
        /resetoilrig all
        ```

    ??? info "/setting"
        **Składnia:** `/setting list [filter]` lub `/setting <setting_name> <get|set|add|sub> [value]`

        **Opis:** Odczytuje lub zmienia obsługiwane wartości `UPalGameSetting` podczas działania gry. Wielkość liter w nazwach nie ma znaczenia; można podać jednoznaczny początek nazwy lub jej fragment. Funkcja jest eksperymentalna i nie zastępuje trwałej konfiguracji świata. Klienci mogą nadal wyświetlać wartości z pamięci podręcznej.

        - `list [filter]`: Wyświetla obsługiwane pola typu całkowitego, zmiennoprzecinkowego, logicznego, bajtowego i wyliczeniowego.
        - `get`: Odczytuje wartość.
        - `set`: Ustawia wartość dowolnego obsługiwanego typu. Wartości logiczne przyjmują `true/false`, `on/off`, `yes/no` lub `1/0`, a typy wyliczeniowe — liczbę lub nazwę elementu.
        - `add` / `sub`: Zmienia wyłącznie wartości liczbowe.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykłady:**
        ```
        /setting list death
        /setting PalDeathPenaltyTime get
        /setting PalDeathPenaltyTime set 10
        ```

    ??? info "/resetbosstower"
        **Składnia:** `/resetbosstower <BossType|all>`

        **Opis:** Polecenie dostępne tylko w kompilacjach Debug. Resetuje jedną instancję wieży bossa lub wszystkie wieże, które można zresetować. Przy wskazywaniu pojedynczego celu należy podać prawidłową nazwę `EPalBossType`. Polecenie nie jest dostępne w publicznych kompilacjach Release.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /resetbosstower all
        ```

    ??? info "/showbosses"
        **Składnia:** `/showbosses`

        **Opis:** Polecenie eksportu danych dostępne tylko w kompilacjach Debug. Zapisuje aktualne dane statyczne bossów w `PalDefender/Logs/BossInfo.json`. Nie jest dostępne w publicznych kompilacjach Release.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

??? note "Zarządzanie bazami"
    ??? info "/findunusedbases (alias: /findbases)"
        **Składnia:** `/findbases [empty|inactive|unused|all] [days=N] [builds<=N]`

        **Składnia interaktywna:** `/findbases visit [filters]`, `/findbases next`, `/findbases kill [next]`

        **Opis:** Wyszukuje puste, nieaktywne lub nieużywane bazy. `visit` tworzy kolejkę do przeglądu dostępną tylko na czacie i teleportuje do pierwszego wyniku; `next` przechodzi do następnego; `kill` niszczy wybraną bazę; `kill next` niszczy ją i przechodzi dalej. Zniszczenie jest nieodwracalne, dlatego najpierw sprawdź każdy cel.

        - `empty`: Brak pracowników, a liczba budowli nie przekracza domyślnego limitu lub `builds<=N`.
        - `inactive`: Brak członków gildii online i brak aktywności przez co najmniej `days` dni (domyślnie `30`).
        - `unused`: Obejmuje bazy puste lub nieaktywne.
        - `all`: Wyświetla wszystkie bazy z uwzględnieniem jawnie podanych filtrów.

        **Uprawnienia:** Wyświetlanie listy obsługuje `Chat` i `RCON`; visit/next/kill wymagają czatu w grze i uprawnień administratora.

        **Przykłady:**
        ```
        /findbases empty builds<=5
        /findbases inactive days=14
        /findbases visit unused days=30
        /findbases kill next
        ```

    ??? info "/getnearestbase"
        **Składnia:** `/getnearestbase [X] [Y] [Z]`

        **Opis:** Wyświetla nazwę gildii będącej właścicielem bazy najbliższej twojej postaci.

        **Uwaga:** Przy wykonywaniu przez **RCON** wszystkie parametry pozycji (`[X]` `[Y]` `[Z]`) **są wymagane**, ponieważ RCON nie ma postaci gracza, na podstawie której można ustalić pozycję.

        **Argumenty:**

        - `[X]`: (Opcjonalnie) Współrzędna X.
        - `[Y]`: (Opcjonalnie) Współrzędna Y.
        - `[Z]`: (Opcjonalnie) Współrzędna Z.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /getnearestbase 100 200 50
        ```

    ??? info "/gotonearestbase"
        **Składnia:** `/gotonearestbase [X] [Y] [Z]`

        **Opis:** Teleportuje do bazy najbliższej podanej pozycji.

        **Uwaga:** Przy wykonywaniu przez **RCON** wszystkie parametry pozycji (`[X]` `[Y]` `[Z]`) **są wymagane**, ponieważ RCON nie ma postaci gracza, na podstawie której można ustalić pozycję.

        **Argumenty:**

        - `[X]`: (Opcjonalnie) Współrzędna X.
        - `[Y]`: (Opcjonalnie) Współrzędna Y.
        - `[Z]`: (Opcjonalnie) Współrzędna Z.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /gotonearestbase 100 200 50
        ```

    ??? info "/killnearestbase"
        **Składnia:** `/killnearestbase [X] [Y] [Z]`

        **Opis:** Niszczy najbliższą bazę (**Używaj ostrożnie!**).

        **Uwaga:** Przy wykonywaniu przez **RCON** wszystkie parametry pozycji (`[X]` `[Y]` `[Z]`) **są wymagane**, ponieważ RCON nie ma postaci gracza, na podstawie której można ustalić pozycję.

        **Argumenty:**

        - `[X]`: (Opcjonalnie) Współrzędna X.
        - `[Y]`: (Opcjonalnie) Współrzędna Y.
        - `[Z]`: (Opcjonalnie) Współrzędna Z.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /killnearestbase 100 200 50
        ```


??? note "Zarządzanie graczami"
    ??? info "/kick"
        **Składnia:** `/kick <UserId> [Reason="Kicked by Admin."]`

        **Opis:** Wyrzuca gracza z serwera.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza do wyrzucenia.
        - `[Reason]`: (Opcjonalnie) Powód wyrzucenia. Domyślnie: "Kicked by Admin." (wyrzucony przez administratora).

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /kick steam_76500000000000000 "Spamowanie na czacie"
        ```

    ??? info "/ban"
        **Składnia:** `/ban <UserId> [Reason="Banned by Admin."]`

        **Opis:** Blokuje gracza i wyrzuca go z serwera.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza do zablokowania.
        - `[Reason]`: (Opcjonalnie) Powód blokady. Domyślnie: "Banned by Admin." (zablokowany przez administratora).

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /ban gdk_25300000000000000 "Oszukiwanie"
        ```

    ??? info "/ipban"
        **Składnia:** `/ipban <UserId> [Reason="Banned by Admin."]`

        **Opis:** Blokuje adres IP gracza, a następnie wyrzuca go z serwera.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza, którego adres IP ma zostać zablokowany.
        - `[Reason]`: (Opcjonalnie) Powód blokady. Domyślnie: "Banned by Admin." (zablokowany przez administratora).

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /ipban steam_76500000000000000
        ```

    ??? info "/banip"
        **Składnia:** `/banip <IP>`

        **Opis:** Blokuje dostęp do serwera z podanego adresu IP.

        **Argumenty:**

        - `<IP>`: Adres IP do zablokowania.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /banip 192.168.1.1
        ```

    ??? info "/unbanip"
        **Składnia:** `/unbanip <IP>`

        **Opis:** Usuwa adres IP z listy blokad.

        **Argumenty:**

        - `<IP>`: Adres IP, którego blokadę należy cofnąć.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /unbanip 192.168.1.1
        ```

    ??? info "/unban"
        **Składnia:** `/unban <UserId> [Reason="Unbanned by admin."]`

        **Opis:** Usuwa UserId z listy blokad PalDefender.

        **Argumenty:**

        - `<UserId>`: UserId gracza, którego blokadę należy cofnąć.
        - `[Reason]`: (Opcjonalnie) Powód zapisany przy cofnięciu blokady.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /unban steam_76500000000000000 "Odwołanie przyjęte"
        ```

    ??? info "/getip"
        **Składnia:** `/getip <UserId>`

        **Opis:** Wyświetla adres IP gracza.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /getip gdk_25300000000000000
        ```

    ??? info "/whitelist_add"
        **Składnia:** `/whitelist_add <UserId>`

        **Opis:** Dodaje UserId do listy dozwolonych graczy.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza do dodania do listy dozwolonych.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /whitelist_add steam_76500000000000000
        ```

    ??? info "/whitelist_remove"
        **Składnia:** `/whitelist_remove <UserId>`

        **Opis:** Usuwa UserId z listy dozwolonych graczy.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza do usunięcia z listy dozwolonych.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /whitelist_remove gdk_25300000000000000
        ```

    ??? info "/whitelist_get"
        **Składnia:** `/whitelist_get`

        **Opis:** Wyświetla pełną listę dozwolonych graczy.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /whitelist_get
        ```

    ??? info "/imcheater"
        **Składnia:** `/imcheater`

        **Opis:** Pozwala sprawdzić, jak serwer reaguje na oszusta.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /imcheater
        ```

    ??? info "/spectate"
        **Składnia:** `/spectate`

        **Opis:** Włącza tryb obserwatora, tak jak skrót klawiszowy `\`. Skrót nie działa jednak u wszystkich, na przykład u graczy na konsolach.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /spectate
        ```

??? note "Postać gracza"
    ??? info "/tp"
        **Składnia:**
        Możesz użyć dowolnej z poniższych wersji:

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

        **Opis:** Teleportuje ciebie lub wskazanego gracza do innego gracza, podanych współrzędnych, najbliższej własnej bazy albo platformy wiertniczej.

        **Uwaga:** W RCON należy wskazać teleportowanego gracza, ponieważ RCON nie ma postaci w grze.

        **Argumenty:**

        - `<UserId>`: Gracz docelowy teleportacji albo teleportowany gracz, jeśli podano więcej argumentów.
        - `<UserId1>`: Teleportowany gracz.
        - `<UserId2>`: Gracz docelowy.
        - `<X> <Y> [Z]`: Współrzędne mapy. Jeśli pominięto `Z`, PalDefender próbuje ustalić odpowiednią wysokość podłoża.
        - `home`: Teleportuje do najbliższej własnej bazy.
        - `oilrig`, `oilrig:Lv30`, `oilrig:Lv55`, `oilrig:Lv60`: Teleportuje do platformy wiertniczej.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /tp steam_76500000000000000 gdk_25300000000000000
        /tp 100 -250
        /tp oilrig:Lv60
        ```

    ??? info "/give_exp"
        **Składnia:** `/give_exp <UserId> <Amount>`

        **Opis:** Przyznaje graczowi punkty doświadczenia.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<Amount>`: Liczba punktów doświadczenia.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /give_exp gdk_25300000000000000 1000
        ```

    ??? info "/giveme_exp"
        **Składnia:** `/giveme_exp <Amount>`

        **Opis:** Przyznaje ci punkty doświadczenia.

        **Argumenty:**

        - `<Amount>`: Liczba punktów doświadczenia.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /giveme_exp 1000
        ```

    ??? info "/renameplayer"
        **Składnia:** `/renameplayer <UserId> <NewName>`

        **Opis:** Zmienia pseudonim gracza.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<NewName>`: Nowy pseudonim.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /renameplayer steam_76500000000000000 NowyPseudonim
        ```

    ??? info "/givestats"
        **Składnia:** `/givestats <UserId> [Count=1]`

        **Opis:** Przyznaje graczowi niewydane punkty atrybutów (wartość ujemna je odejmuje). Nie zmienia już wydanych punktów.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza otrzymującego punkty atrybutów.
        - `[Count]`: (Opcjonalnie) Liczba niewydanych punktów atrybutów do przyznania (ujemna wartość odejmuje punkty). Domyślnie: 1.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /givestats steam_76500000000000000 5
        /givestats steam_76500000000000000 -2
        ```

    ??? info "/givemestats"
        **Składnia:** `/givemestats [Count=1]`

        **Opis:** Przyznaje ci niewydane punkty atrybutów (wartość ujemna je odejmuje). Nie zmienia już wydanych punktów.

        **Argumenty:**

        - `[Count]`: (Opcjonalnie) Liczba niewydanych punktów atrybutów do przyznania sobie (ujemna wartość odejmuje punkty). Domyślnie: 1.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemestats 5
        /givemestats -2
        ```

    ??? info "/godmode"
        **Składnia:** `/godmode [on/off]`

        **Opis:** Zapewnia nietykalność i odporność na efekty statusu, blokuje zużywanie jedzenia i przywraca zdrowie przy aktywacji. Jeśli włączono to w konfiguracji, może również pozwalać na zabijanie wszystkiego jednym trafieniem.

        **Argumenty:**

        - `[on/off]`: (Opcjonalnie) Jawne włączenie lub wyłączenie trybu nieśmiertelności. Domyślnie: przełącza stan.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /godmode
        /godmode on
        /godmode off
        ```

    ??? info "/admingun (alias: /agun)"
        **Składnia:** `/admingun`

        **Opis:** Daje aktywnemu administratorowi w grze chronioną broń Admin Gun. Natychmiast zabija postacie, niszczy obiekty mapy, zadaje maksymalne obrażenia roślinności i ma nieograniczoną amunicję oraz wytrzymałość. Nie można jej wyrzucić, sprzedać ani przenieść do zewnętrznych pojemników. Kucnij podczas niszczenia pojemnika, aby usunąć jego zawartość; pozostań w pozycji stojącej, aby ją zachować. Broń znika po śmierci, wylogowaniu z gry lub wyłączeniu trybu administratora. Ponowne wywołanie polecenia zastępuje poprzedni egzemplarz.

        **Uprawnienia:** `Chat`, aktywny status administratora w grze. `allowAdminCheats` nie jest wymagane.

        **Przykład:**
        ```
        /agun
        ```

??? note "Zarządzanie gildiami"
    ??? info "/setguildleader"
        **Składnia:** `/setguildleader <UserId>`

        **Opis:** Ustanawia wskazanego gracza liderem jego obecnej gildii.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza, który ma zostać liderem gildii.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /setguildleader gdk_25300000000000000
        ```

    ??? info "/exportguilds"
        **Składnia:** `/exportguilds`

        **Opis:** Eksportuje wszystkie gildie serwera do Pal/Binaries/Win64/PalDefender/guildexport.json.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /exportguilds
        ```
        Przykładowy plik wynikowy: `Pal/Binaries/Win64/PalDefender/guildexport.json`


??? note "Przedmioty"
    ??? info "/give"
        **Składnia:** `/give <UserId> <ItemId> [Amount=1]`

        **Opis:** Daje graczowi przedmiot w podanej liczbie.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza otrzymującego przedmiot.
        - `<ItemId>`: Przedmiot do przyznania.
        - `[Amount]`: (Opcjonalnie) Liczba sztuk. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /give steam_76500000000000000 Sword 2
        ```

    ??? info "/giveitems"
        **Składnia:** `/giveitems <UserId> <ItemId>[:<Amount>] ...`

        **Opis:** Daje graczowi kilka przedmiotów jednym poleceniem. Liczbę sztuk każdego przedmiotu można podać po dwukropku.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza otrzymującego przedmioty.
        - `<ItemId>[:<Amount>] ...`: Lista przedmiotów i opcjonalnych liczebności.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /giveitems gdk_25300000000000000 Sword:2 Shield:1
        ```

    ??? info "/giveme"
        **Składnia:** `/giveme <ItemId> [Amount=1]`

        **Opis:** Daje ci przedmiot w podanej liczbie.

        **Argumenty:**

        - `<ItemId>`: Przedmiot do przyznania sobie.
        - `[Amount]`: (Opcjonalnie) Liczba sztuk. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /giveme Sword 3
        ```

    ??? info "/delitem"
        **Składnia:** `/delitem <UserId> <ItemId> [Amount=1]`

        **Opis:** Usuwa przedmiot gracza w podanej liczbie. Domyślnie `1` usuwa jedną sztukę. Użyj `all` zamiast `1`, aby usunąć wszystkie sztuki.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<ItemId>`: Przedmiot do usunięcia.
        - `[Amount]`: (Opcjonalnie) Liczba sztuk. Domyślnie: 1. Użyj `all`, aby usunąć wszystkie.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /delitem steam_76500000000000000 Sword 1
        /delitem gdk_25300000000000000 Sword all
        ```

    ??? info "/give_relic"
        **Składnia:** `/give_relic <UserId> <RelicType> [Amount]`

        **Opis:** Przyznaje graczowi punkty reliktów wybranego typu.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza otrzymującego punkty reliktów.
        - `<RelicType>`: Typ przyznawanych punktów reliktów.

        - `[Amount]`: Opcjonalna liczba przyznawanych punktów reliktów. Domyślnie `1`.

        **Obsługiwane typy reliktów:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /give_relic steam_76500000000000000 CapturePower 5
        ```

    ??? info "/giveme_relic"
        **Składnia:** `/giveme_relic <RelicType> [Amount]`

        **Opis:** Przyznaje ci punkty reliktów wybranego typu.

        **Argumenty:**

        - `<RelicType>`: Typ przyznawanych punktów reliktów.

        - `[Amount]`: Opcjonalna liczba punktów reliktów do przyznania sobie. Domyślnie `1`.

        **Obsługiwane typy reliktów:** `CapturePower`, `HungerReduction`, `SwimSpeed`, `FoodDecayReduction`, `JumpPower`, `GliderSpeed`, `ClimbSpeed`, `StatusAilmentResist`, `StaminaReduction`, `SphereHoming`, `ExpBonus`, `RainbowPassiveRate`, `MoveSpeed`.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /giveme_relic CapturePower 5
        ```


    ??? info "/delitems"
        **Składnia:** `/delitems <UserId> <ItemId>[:<Amount>] ...`

        **Opis:** Usuwa kilka przedmiotów gracza jednym poleceniem. Liczbę sztuk każdego przedmiotu można podać po dwukropku. Użyj `all` zamiast `1`, aby usunąć wszystkie sztuki.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<ItemId>[:<Amount>] ...`: Lista przedmiotów i opcjonalnych liczebności.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /delitems steam_76500000000000000 Sword:1 Shield:all
        ```

    ??? info "/clearinv"
        **Składnia:** `/clearinv <UserId> [Container=items] ...`

        **Opis:** Opróżnia wskazane pojemniki w ekwipunku gracza. Dostępne pojemniki: `items`, `keyitems`, `armor`, `weapons`, `food`, `dropslot` lub `all`.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `[Container] ...`: (Opcjonalnie) Pojemniki do opróżnienia. Domyślnie: items.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /clearinv steam_76500000000000000 items
        /clearinv gdk_25300000000000000 all
        ```


??? note "Pale"
    ??? info "/givepal"
        **Składnia:** `/givepal <UserId> <PalId> [Level=1]`

        **Opis:** Daje graczowi Pala na wskazanym poziomie.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<PalId>`: Pal do przyznania.
            - **Uwaga:** Użyj identyfikatora Pala, na przykład `WeaselDragon` (Chillet). Pełna lista jest dostępna na [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Opcjonalnie) Poziom Pala. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /givepal gdk_25300000000000000 WeaselDragon 10
        ```

    ??? info "/givepal_j"
        **Składnia:** `/givepal_j <UserID> <PalTemplate>`

        **Opis:** Daje graczowi Pala zdefiniowanego w pliku [PalTemplate](../FileTypes/PalTemplate.md). Osadzony JSON nie jest już obsługiwany; należy podać nazwę pliku.

        **Uwaga:** Nie musisz podawać rozszerzenia .json w nazwie pliku; system automatycznie je dopisze, jeśli go brakuje.

        **Argumenty:**

        - `<UserID>`: Identyfikator gracza.
        - `<PalTemplate>`: Nazwa pliku PalTemplate (zobacz [PalTemplate](../FileTypes/PalTemplate.md)).

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /givepal_j steam_76500000000000000 MyPalTemplate
        ```

    ??? info "/givemepal"
        **Składnia:** `/givemepal <PalId> [Level=1]`

        **Opis:** Daje ci Pala na wskazanym poziomie.

        **Argumenty:**

        - `<PalId>`: Pal do przyznania sobie.
            - **Uwaga:** Użyj identyfikatora Pala, na przykład `WeaselDragon` (Chillet). Pełna lista jest dostępna na [paldeck.cc/pals](https://paldeck.cc/pals).
        - `[Level]`: (Opcjonalnie) Poziom Pala. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemepal WeaselDragon 10
        ```

    ??? info "/givemepal_j"
        **Składnia:** `/givemepal_j <PalTemplate>`

        **Opis:** Daje ci Pala zdefiniowanego w pliku [PalTemplate](../FileTypes/PalTemplate.md). Osadzony JSON nie jest już obsługiwany; należy podać nazwę pliku.

        **Argumenty:**

        - `<PalTemplate>`: Nazwa pliku PalTemplate (zobacz [PalTemplate](../FileTypes/PalTemplate.md)).

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemepal_j MyPalTemplate
        ```

    ??? info "/spawnpal"
        **Składnia:**
        Możesz użyć dowolnej z poniższych wersji:

        - `/spawnpal <PalID>`
        - `/spawnpal <PalID> [Level]`
        - `/spawnpal <PalID> [x] [y] [z]`
        - `/spawnpal <PalID> [x] [y] [z] [Level]`

        **Opis:** Tworzy Pala w pozycji względnej do twojej postaci lub pod podanymi współrzędnymi bezwzględnymi. **W RCON należy podać x, y i z!**

        **Uwaga:** Wszystkie statystyki poza poziomem są losowane.

        **Argumenty:**
        - `<PalID>`: Pal do utworzenia.
        - `[x]`: (Opcjonalnie) Pozycja x Pala. Domyślnie: względem gracza wywołującego polecenie.
        - `[y]`: (Opcjonalnie) Pozycja y Pala. Domyślnie: względem gracza wywołującego polecenie.
        - `[z]`: (Opcjonalnie) Pozycja z Pala. Domyślnie: względem gracza wywołującego polecenie.
        - `[Level]`: (Opcjonalnie) Poziom Pala. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /spawnpal Anubis 255
        ```
        _Tworzy Anubisa na poziomie 255!_

    ??? info "/spawnpal_ex"
        **Składnia:** Tak jak `/spawnpal`.

        **Opis:** Tworzy Pala tak jak `/spawnpal`, ale włącza śledzenie obrażeń. Gdy Pal zginie lub zostanie schwytany, PalDefender zapisuje pełny ranking obrażeń i wysyła go do `PalWebhooks.webhookURL_Summons`, jeśli skonfigurowano ten webhook. Przy włączonym `announceAdminSummonsKill` uczestniczący gracze online otrzymują również okno wyników z pierwszą piątką i własnym miejscem. Zwycięzcą zostaje gracz, który zadał najwięcej obrażeń. Polecenie nie używa pliku PalTemplate ani PalSummon i nie przyznaje nagród.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /spawnpal_ex Anubis 230 -486 4097 80
        ```

    ??? info "/spawnnpc"
        **Składnia:** `/spawnnpc <NPCID|CharacterID> [Level=1]` lub `/spawnnpc <NPCID|CharacterID> <X> <Y> [Z] [Level=1]`

        **Opis:** Tworzy NPC ze sztuczną inteligencją. Na czacie pominięcie współrzędnych powoduje utworzenie NPC w pobliżu administratora; w RCON współrzędne są wymagane. Przy podaniu tylko `X` i `Y` PalDefender ustala wysokość podłoża.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /spawnnpc PIDF_Soldier_AssaultRifle 30
        ```

    ??? info "/spawnpal_j"
        **Składnia:**

        Możesz użyć dowolnej z poniższych wersji:

        - `/spawnpal_j <PalTemplate>`
        - `/spawnpal_j <PalTemplate> [x] [y] [z]`

        **Opis:** Tworzy Pala w pozycji względnej do twojej postaci lub pod podanymi współrzędnymi bezwzględnymi. **W RCON należy podać x, y i z!**

        **Uwaga:** Używa atrybutów z pliku [PalTemplate](../FileTypes/PalTemplate.md) w `Pals/Templates/`, podobnie jak `/givepal_j` i polecenia jaj korzystające z szablonów. Aby utworzyć pełne starcie z opcjami przywołania i nagrodami, użyj `/summon` z plikiem [PalSummon](../FileTypes/PalSummon.md). `/spawnpal` przyjmuje identyfikator Pala, a nie nazwę szablonu.

        **Argumenty:**

        - `<PalTemplate>`: Nazwa używanego pliku [PalTemplate](../FileTypes/PalTemplate.md).
        - `[x]`: (Opcjonalnie) Pozycja x Pala. Domyślnie: względem gracza wywołującego polecenie.
        - `[y]`: (Opcjonalnie) Pozycja y Pala. Domyślnie: względem gracza wywołującego polecenie.
        - `[z]`: (Opcjonalnie) Pozycja z Pala. Domyślnie: względem gracza wywołującego polecenie.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /spawnpal_j ArenaBoss 230 -486 4097
        ```

    ??? info "/spawnpal_ex_j"
        **Składnia:** `/spawnpal_ex_j <PalTemplate> [x] [y] [z]`

        **Opis:** Używa tego samego pliku [PalTemplate](../FileTypes/PalTemplate.md) i obsługi współrzędnych co `/spawnpal_j`, ale włącza śledzenie obrażeń. Gdy Pal zginie lub zostanie schwytany, PalDefender zapisuje pełny ranking obrażeń i wysyła go do `PalWebhooks.webhookURL_Summons`, jeśli skonfigurowano ten webhook. Przy włączonym `announceAdminSummonsKill` uczestniczący gracze online otrzymują również okno wyników z pierwszą piątką i własnym miejscem. Zwycięzcą zostaje gracz, który zadał najwięcej obrażeń. Polecenie nie korzysta z nagród [PalSummon](../FileTypes/PalSummon.md).

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /spawnpal_ex_j ArenaBoss 230 -486 4097
        ```

    ??? info "/summon"
        **Składnia:** `/summon <PalSummon>`

        **Opis:** Tworzy Pala przy użyciu wskazanego pliku [PalSummon](../FileTypes/PalSummon.md).

        **Uwaga:** Nie musisz podawać rozszerzenia .json w nazwie pliku; system automatycznie je dopisze, jeśli go brakuje.

        **Argumenty:**
        - `<PalSummon>`: Nazwa pliku [PalSummon](../FileTypes/PalSummon.md) w `PalDefender/Pals/Summons/`, **nie** nazwa pliku [PalTemplate](../FileTypes/PalTemplate.md). Plik wskazuje szablon PalTemplate z atrybutami Pala i dodaje opcje przywołania, takie jak współrzędne oraz opcjonalne nagrody. Na przykład `/summon ArenaEncounter` wczytuje `Pals/Summons/ArenaEncounter.json`.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /summon PalSummon
        ```

    ??? info "/giveegg"
        **Składnia:** `/giveegg <UserId> <EggId> <PalId> [Level]`

        **Opis:** Daje wskazanemu graczowi jajo z określonym Palem, opcjonalnie na zmienionym poziomie.

        **Argumenty:**

        ??? quote "<UserId\>"
            **Opis:** Identyfikator gracza otrzymującego jajo.

        ??? quote "<EggId\>"
            **Opis:** Typ przyznawanego jaja.

            **Uwaga:** Dla każdego typu dozwolone są wartości od 01 (najmniejsze) do 05 (największe):

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
            **Opis:** Pal znajdujący się w jaju.

            **Uwaga:** Użyj identyfikatora Pala, na przykład `WeaselDragon` (Chillet). Pełna lista jest dostępna na [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level\]"
            **Opis:** (Opcjonalnie) Poziom Pala w jaju.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /giveegg steam_76500000000000000 PalEgg_Ice_01 WeaselDragon 10
        ```


    ??? info "/givemeegg"
        **Składnia:** `/givemeegg <EggId> <PalId> [Level]`

        **Opis:** Daje ci jajo z określonym Palem, opcjonalnie na zmienionym poziomie.

        **Argumenty:**

        ??? quote "<EggId\>"
            **Opis:** Typ jaja do przyznania sobie.

            **Uwaga:** Dla każdego typu dozwolone są wartości od 01 (najmniejsze) do 05 (największe):

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
            **Opis:** Pal znajdujący się w jaju.

            **Uwaga:** Użyj identyfikatora Pala, na przykład `WeaselDragon` (Chillet). Pełna lista jest dostępna na [paldeck.cc/pals](https://paldeck.cc/pals).

        ??? quote "[Level]"
            **Opis:** (Opcjonalnie) Poziom Pala w jaju.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemeegg PalEgg_Ice_01 WeaselDragon 10
        ```

    ??? info "/giveegg_j"
        **Składnia:** `/giveegg_j <EggId> <PalTemplate> [Level]`

        **Opis:** Daje jajo z Palem zdefiniowanym w pliku [PalTemplate](../FileTypes/PalTemplate.md), opcjonalnie na zmienionym poziomie.

        **Argumenty:**

        ??? quote "<EggId\>"
            **Opis:** Typ przyznawanego jaja.

            **Uwaga:** Dla każdego typu dozwolone są wartości od 01 (najmniejsze) do 05 (największe):

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
            **Opis:** Nazwa używanego pliku [PalTemplate](../FileTypes/PalTemplate.md).

            **Uwaga:** Nie musisz podawać rozszerzenia .json w nazwie pliku; system automatycznie je dopisze, jeśli go brakuje. Zobacz [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Level]"
            **Opis:** (Opcjonalnie) Poziom Pala w jaju.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /giveegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/givemeegg_j"
        **Składnia:** `/givemeegg_j <EggId> <PalTemplate> [Level]`

        **Opis:** Daje ci jajo z Palem zdefiniowanym w pliku [PalTemplate](../FileTypes/PalTemplate.md), opcjonalnie na zmienionym poziomie.

        **Argumenty:**

        ??? quote "<EggI\>"
            **Opis:** Typ jaja do przyznania sobie.

            **Uwaga:** Dla każdego typu dozwolone są wartości od 01 (najmniejsze) do 05 (największe):

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
            **Opis:** Nazwa używanego pliku [PalTemplate](../FileTypes/PalTemplate.md).

            **Uwaga:** Nie musisz podawać rozszerzenia .json w nazwie pliku; system automatycznie je dopisze, jeśli go brakuje. Zobacz [PalTemplate](../FileTypes/PalTemplate.md).

        ??? quote "[Level]"
            **Opis:** (Opcjonalnie) Poziom Pala w jaju.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemeegg_j PalEgg_Ice_01 MyPalTemplate 10
        ```

    ??? info "/jetragon"
        **Składnia:** `/jetragon`

        **Opis:** Daje ci administracyjnego Jetragona (jest tak szybki, że… już go nie ma).

        **Argumenty:**
        - Brak

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /jetragon
        ```

    ??? info "/catwaifu"
        **Składnia:** `/catwaifu`

        **Opis:** Daje ci administracyjną Cat-Waifu wzmacniającą statystyki twojej postaci.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /catwaifu
        ```

    ??? info "/exportpals"
        **Składnia:** `/exportpals [UserId]`

        **Opis:** Eksportuje wszystkie Pale gracza do plików [PalTemplate](../FileTypes/PalTemplate.md) w Pal/Binaries/Win64/PalDefender/pals/exported/<UserId>/.

        **Argumenty:**

        - `[UserId]`: (Opcjonalnie) Identyfikator gracza, którego Pale mają zostać wyeksportowane. Pominięcie powoduje eksport twoich Pali.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /exportpals steam_76500000000000000
        /exportpals
        ```

    ??? info "/deletepals"
        **Składnia:** `/deletepals <UserId> <PalFilter>`

        **Opis:** Usuwa Pale wskazanego gracza przy użyciu zaawansowanych filtrów. Jedno polecenie może uwzględniać wiele kryteriów, na przykład identyfikator Pala, poziom, płeć i umiejętności pasywne. Przetestuj działanie w bezpiecznym środowisku przed użyciem na ważnych danych.

        **Argumenty:**

        ??? quote "<UserId\>"
            **Opis:** Identyfikator gracza, którego Pale zostaną usunięte.

        ??? quote "<PalFilter\>"
            **Opis:** Zestaw słów kluczowych filtra określających Pale do usunięcia.

            **Uwaga:** W jednym poleceniu można połączyć kilka słów kluczowych.

            Dostępne słowa kluczowe filtra:

            - `ID`: PalID lub lista PalID rozdzielonych przecinkami
            - `Nick`: Ciąg znaków (nazwa Pala)
            - `Gender`: `male` lub `female`
            - `Level`: Liczba; obsługiwane operatory: `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Rank`: Liczba; obsługiwane operatory: `<`, `>`, `<=`, `>=`, `=`, `!=`
            - `Lucky`: `true` lub `false` (szczęśliwy Pal)
            - `Passives`: PassiveSkill lub lista PassiveSkill rozdzielonych przecinkami
            - `Limit`: Liczba (maksymalna liczba Pali do usunięcia)

            **Przykładowe filtry:**

            - `ID Serpent, PinkLizard Level>10 Gender male Limit 3`
            - `ID Anubis Rank>=3`
            - `Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave`

            Powyższe klucze i przykłady przedstawiają aktualną składnię PalFilter.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /deletepals 76567890987654321 ID Serpent, PinkLizard Level>10 Gender male Limit 3
        /deletepals 76567890987654321 ID Anubis Rank>=3
        /deletepals 76561198033277828 Passives CraftSpeed_up1,CraftSpeed_up2,Rare,PAL_CorporateSlave
        ```


??? note "Drzewo technologii"
    ??? info "/learntech"
        **Składnia:** `/learntech <UserId> <TechID>`

        **Opis:** Odblokowuje graczowi wskazaną technologię. Użyj `all`, aby odblokować wszystkie.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<TechID>`: Technologia do odblokowania. Użyj `all`, aby odblokować wszystkie.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /learntech steam_76500000000000000 Tech001
        /learntech gdk_25300000000000000 all
        ```

    ??? info "/unlearntech"
        **Składnia:** `/unlearntech <UserId> <TechID>`

        **Opis:** Usuwa wskazaną technologię z poznanych technologii gracza. Użyj `all`, aby usunąć wszystkie.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza.
        - `<TechID>`: Technologia do usunięcia. Użyj `all`, aby usunąć wszystkie.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /unlearntech gdk_25300000000000000 Tech001
        /unlearntech steam_76500000000000000 all
        ```

    ??? info "/givetechpoints"
        **Składnia:** `/givetechpoints <UserId> [Amount=1]`

        **Opis:** Przyznaje wskazanemu graczowi X punktów technologii.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza otrzymującego punkty technologii.
        - `[Amount]`: (Opcjonalnie) Liczba przyznawanych punktów technologii. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /givetechpoints steam_76500000000000000 10
        ```

    ??? info "/givebosstechpoints"
        **Składnia:** `/givebosstechpoints <UserId> [Amount=1]`

        **Opis:** Przyznaje wskazanemu graczowi X punktów starożytnej technologii.

        **Argumenty:**

        - `<UserId>`: Identyfikator gracza otrzymującego punkty starożytnej technologii.
        - `[Amount]`: (Opcjonalnie) Liczba przyznawanych punktów starożytnej technologii. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /givebosstechpoints steam_76500000000000000 5
        ```

    ??? info "/givemetechpoints"
        **Składnia:** `/givemetechpoints [Amount=1]`

        **Opis:** Przyznaje ci X punktów technologii.

        **Argumenty:**

        - `[Amount]`: (Opcjonalnie) Liczba punktów technologii do przyznania sobie. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemetechpoints 10
        ```

    ??? info "/givemebosstechpoints"
        **Składnia:** `/givemebosstechpoints [Amount=1]`

        **Opis:** Przyznaje ci X punktów starożytnej technologii.

        **Argumenty:**

        - `[Amount]`: (Opcjonalnie) Liczba punktów starożytnej technologii do przyznania sobie. Domyślnie: 1.

        **Uprawnienia:** `Chat`, `Admin`

        **Przykład:**
        ```
        /givemebosstechpoints 5
        ```


??? note "Eksport danych"
    ??? info "/gettechids"
        **Składnia:** `/gettechids`

        **Opis:** Zwraca listę wszystkich dostępnych identyfikatorów technologii. RCON zwraca wynik w formacie JSON.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /gettechids
        ```

    ??? info "/getskinids"
        **Składnia:** `/getskinids`

        **Opis:** Zwraca listę wszystkich dostępnych identyfikatorów skórek Pali. RCON zwraca wynik w formacie JSON.

        **Argumenty:**

        - Brak

        **Uprawnienia:** `Chat`, `RCON`, `Admin`

        **Przykład:**
        ```
        /getskinids
        ```
