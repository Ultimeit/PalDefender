# PalDefender REST API

Ta sekcja opisuje wbudowane REST API PalDefender — niewielki interfejs HTTP przeznaczony do użytku **lokalnego lub w zaufanym środowisku**.

- **Domyślny bazowy adres URL:** `http://127.0.0.1:17993`
- **Uwierzytelnianie:** token Bearer (wymagany dla wszystkich punktów końcowych)
- **Punkt końcowy wersji:** `/v1/pdapi/version`

> Uwaga dotycząca bezpieczeństwa: **nie** udostępniaj tego portu bezpośrednio w internecie. Jeśli potrzebujesz zdalnego dostępu, użyj odwrotnego serwera proxy i odpowiedniej kontroli dostępu.

## Zawartość tej sekcji
- [Uwierzytelnianie i konfiguracja](authentication.md)
- [Punkty końcowe](Endpoints/index.md)
