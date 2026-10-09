# Foldery projektu i uruchamianie

Projekt znajduje się w `C:\Users\MP\Documents\ChatGPT\Opisy Erli`.

| Folder | Zawartość |
| --- | --- |
| `scripts/allegro` | Autoryzacja Allegro i odczyt przykładowych składów |
| `scripts/base` | Konfiguracja Base, odczyt katalogu i uzupełnianie parametru INCI |
| `scripts/erli` | Konfiguracja ERLI, odczyt ofert, aktualizacja opisów i weryfikacja |
| `scripts/lib` | Wspólne funkcje API, dopasowania produktów, układ opisów i ścieżki plików |
| `config` | Zaszyfrowane dane dostępowe DPAPI i identyfikator User-Agent |
| `data/allegro` | Pobrane próbki ofert Allegro |
| `data/base` | Dane produktów Base oraz plan zmian w JSON i CSV |
| `data/erli` | Dane ofert ERLI, schemat API oraz plan zmian w JSON i CSV |
| `data/archive` | Wcześniejsze plany i potwierdzenia oraz spis przeniesionych plików |
| `backups/base` | Kopie produktów Base sprzed zapisów |
| `backups/erli` | Kopie ofert ERLI sprzed zapisów |
| `reports/base` | Wyniki aktualizacji i podsumowanie Base |
| `reports/erli` | Wyniki aktualizacji, podsumowanie i potwierdzenie odczytu ERLI |
| `doc` | Dokumentacja aplikacji, ta instrukcja i lokalny raport wykonanych zmian |
| `tests` | Lokalne testy autoryzacji, synchronizacji, układu INCI i ścieżek |

Główny `README.md` zawiera odnośniki do dokumentacji. Dane dostępowe, kod roboczy, dane produktów, kopie i raporty pozostają lokalnie. Publiczne repozytorium zawiera wyłącznie `.gitignore`, główny README oraz `doc/README.md` i `doc/STRUKTURA.md`. Lokalny raport `doc/RAPORT-INCI.md` jest wykluczony z Git.

## Uruchamianie

Skrypty ustalają położenie projektu na podstawie własnego pliku, więc można uruchamiać je z dowolnego folderu PowerShell. Zmienione zostały ścieżki do skryptów, a dane dostępowe są nadal odczytywane z istniejących zaszyfrowanych plików.

Poniższe polecenia uruchamiaj w głównym folderze projektu:

```powershell
Set-Location -LiteralPath 'C:\Users\MP\Documents\ChatGPT\Opisy Erli'
```

### Konfiguracja dostępu

Te skrypty są potrzebne przy pierwszej konfiguracji lub zmianie danych dostępowych:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\allegro\allegro-autoryzacja.ps1'
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\base\base-konfiguracja.ps1'
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\erli\erli-konfiguracja.ps1'
```

### Allegro → Base

Podgląd dopasowań i brakujących składów zapisuje się w `data/base`:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\base\sync-inci.ps1'
```

Zastosowanie sprawdzonego planu do pustych parametrów Base:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\base\sync-inci.ps1' -Apply
```

### Base → opisy ERLI

Podgląd zapisuje się w `data/erli`. Dla opisów z dwiema sekcjami INCI trafia do osobnej trzeciej; znany blok dodany poprzednią wersją do drugiej sekcji jest przenoszony. Opcja `-SingleSection Append` zachowuje ustalone dopisywanie na końcu opisów jednosekcyjnych:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\erli\erli-sync-inci.ps1' -SingleSection Append
```

Zastosowanie przygotowanego planu i późniejsza weryfikacja:

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\erli\erli-sync-inci.ps1' -Apply
powershell -NoProfile -ExecutionPolicy Bypass -File '.\scripts\erli\erli-inci-weryfikacja.ps1'
```

Skrypty zapisujące zmiany tworzą kopie w `backups` oraz wyniki w `reports`. Plany do zapisu muszą być świeże; szczegóły zabezpieczeń opisuje [dokumentacja aplikacji](README.md).

### Testy lokalne

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File '.\tests\verify-layout.ps1'
powershell -NoProfile -ExecutionPolicy Bypass -File '.\tests\verify-autoryzacja.ps1'
powershell -NoProfile -ExecutionPolicy Bypass -File '.\tests\verify-sync-inci.ps1'
powershell -NoProfile -ExecutionPolicy Bypass -File '.\tests\verify-erli-inci.ps1'
```

Testy używają lokalnych danych i fikcyjnych odpowiedzi HTTP. Nie zmieniają produktów ani ofert.
