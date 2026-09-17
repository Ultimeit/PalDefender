# Funkcje i aktualny stan

Ta strona podsumowuje funkcje konfigurowane przez użytkownika w PalDefender 1.9.1. Dokładne wartości domyślne znajdziesz w opisie [`Config.json`](./FileTypes/Config.md).

## Aktywna ochrona

- Wykrywanie oszustw związanych z obrażeniami, wytrzymałością, amunicją i duplikowaniem baz można włączać niezależnie.
- Anti-Vacuum blokuje podejrzane próby zbierania z dużej odległości zwykłych przedmiotów, jaj Palów, reliktów i notatek. Gdy `allowAdminCheats` jest włączone, administratorzy omijają obsługiwane kontrole.
- Kontrole nieprawidłowych przedmiotów, statystyk Palów, receptur stanowisk rzemieślniczych, nadużyć związanych z Doctor Surgi, awaryjnego odradzania i innych akcji serwera pozostają częścią wspólnej warstwy weryfikacji.
- `BannedCampWorker` uniemożliwia przypisywanie do bazy postaci o wskazanych identyfikatorach Character ID.

Starsza funkcja sterowana kluczami `antiDupe...` nie jest kompilowana do obecnego wydania. Nowszy mechanizm wykrywania duplikowania baz działa oddzielnie i jest sterowany przez `baseCampDupeDetectionEnabled`.

## Administracja i wydarzenia

- `/admingun` (`/agun`) daje administratorowi z aktywnymi uprawnieniami zabezpieczoną [broń administratora](./Commands/index.md).
- `/setting` pozwala odczytywać lub tymczasowo zmieniać obsługiwane ustawienia działającej gry Palworld.
- `/findbases` tworzy interaktywną kolejkę do przeglądania pustych lub nieaktywnych baz.
- PalSummon obsługuje nazwy walk, ustawienia AI i pomiaru obrażeń, mnożniki statystyk, warunkowe chwytanie, wyniki rankingu i konfigurowalne nagrody. Zobacz [`PalSummon.json`](./FileTypes/PalSummon.md).
- Miejsca docelowe na Discordzie konfiguruje się w `PalWebhooks`. Obsługują czat, polecenia, zgony, dołączanie i opuszczanie serwera, przywołania, wydarzenia na platformach wiertniczych i wykryte oszustwa.

## Sygnał aktywności (heartbeat)

Wydania Release wysyłają sygnał aktywności do `https://pallink.net/api/heartbeat` co 10 sekund po zakończeniu przygotowania gry. Dane obejmują GUID świata/serwera, kod kraju z ustawień regionalnych systemu, wersje PalDefender i Palworld, platformę Windows/Wine/Proton, czas działania procesu oraz liczbę graczy: aktualnie online, maksymalną i łączną liczbę unikalnych graczy. Nie zawierają nazw graczy, identyfikatorów kont, adresów IP graczy, wiadomości czatu ani zawartości zapisów gry. W kompilacjach Debug ten mechanizm jest wyłączony.

## REST API

REST API wymagające uwierzytelnienia pozwala zarządzać graczami, Palami, ekwipunkiem, technologiami, postępami, gildiami, banami, wiadomościami, nagrodami i moderacją. Wersja 1.9.0 dodaje także [`POST /summon/pal`](./RESTAPI/Endpoints/summon-pal.md) i [`POST /summon/npc`](./RESTAPI/Endpoints/summon-npc.md).
