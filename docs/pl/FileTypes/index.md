# 📁 Typy plików

**PalDefender** obsługuje różne pliki konfiguracyjne, które pozwalają zmieniać działanie serwera i rozszerzać jego funkcje.
Obecnie obsługiwane:
* `Config.json`
* `WhiteList.json`
* `Banlist.json`
* `PalTemplate.json`
* `PalSummon.json`
* `Pals/ImportRules/*.json`
* `RESTAPI/RESTConfig.json`
* `RESTAPI/Tokens/*.json`

---

## ⚡ Krótki przegląd

### 🛠️ [Config.json](./Config.md)

Steruje działaniem serwera, moderacją, logami i ustawieniami administratora.

* **Bezpieczeństwo:** ochrona przed oszustwami (ostrzeżenia, wyrzucanie, bany, blokady IP), filtrowanie nazw i słów, ochrona SteamID, sprawdzanie niedozwolonych statystyk i przedmiotów.
* **Logi:** zapis czatu, RCON, logowania, zgonów, przywołań, budowania i wydarzeń na platformach wiertniczych.
* **Administracja:** lista dozwolonych adresów IP, automatyczne logowanie, tryb nieśmiertelności/cheaty, widoczność działań administratora.
* **Ogłoszenia:** wiadomości powitalne MOTD, zgony graczy, przywołania, kary i wydarzenia związane z łupami.
* **Ograniczenia czatu i rozgrywki:** długość wiadomości, pomijanie czasu oczekiwania, limity obrażeń PvP/PvE, ograniczenie wycinania drzew.
* **Pozostałe:** obsługa Base64 w RCON, reakcja na błędy uruchamiania, opcjonalny tryb poleceń w języku chińskim.

---

### 👥 `WhiteList.json`

Określa, kto może dołączyć do serwera.
Obsługuje **identyfikatory użytkowników** i **adresy IP**, w tym zakresy z symbolami wieloznacznymi.

---

### 🚫 `Banlist.json`

Przechowuje wpisy banów PalDefender używane do banowania, usuwania banów, blokowania IP i nakładania kar przez REST API.

* Zamiast ręcznie edytować plik, używaj `/ban`, `/unban`, `/banip`, `/unbanip` lub REST API.
* Jeśli musisz edytować go ręcznie, najpierw zatrzymaj serwer albo po zmianach wczytaj ponownie konfigurację.

---

### 🧬 [PalTemplate.json](./PalTemplate.md)

Służy do tworzenia lub przyznawania niestandardowych Palów za pomocą poleceń.

* Określa **ID, pseudonim, płeć, statystyki (HP/SP/MP), sytość, SAN, rzadkość, umiejętności, wartości indywidualne (IV), cechy pasywne** i inne właściwości Pala.
* Pozwala dostosować **zdolności bojowe, użytkowe i predyspozycje do pracy** Pala.

---

### 📍 [PalSummon.json](./PalSummon.md)

Tworzy niestandardowego Pala we wskazanym miejscu.

* Odwołuje się do `PalTemplate` i ustawia **pozycję w świecie (X, Y, Z)**.
* Ustawia opcje takie jak **brak możliwości schwytania** i wyłącza wybrane **efekty statusu**, np. zatrucie, tonięcie czy podpalenie.

---

### 🧾 [Pals/ImportRules/*.json](./PalImportRules.md)

Określa zasady przyjmowania niestandardowych szablonów Palów.

* Ustaw globalne limity w `Pals/ImportRules/Default.json`.
* Dodaj wyjątki dla konkretnych Palów w plikach takich jak `Pals/ImportRules/Anubis.json`.
* Wybierz, czy przekroczenie limitu blokuje import, czy powoduje obniżenie wartości do maksimum.
* Wybierz, czy niedozwolone cechy pasywne blokują import, czy są usuwane.

---

### 🌐 Pliki konfiguracyjne REST API

Konfiguracja REST API znajduje się w `RESTAPI/RESTConfig.json`, a tokeny Bearer w `RESTAPI/Tokens/*.json`.

* `RESTConfig.json` określa, czy API jest włączone, adres nasłuchiwania, port, logowanie do konsoli i ustawienia CORS.
* Każdy plik tokena powinien zawierać tajny token i uprawnienia. Nie udostępniaj tokenów publicznie.
