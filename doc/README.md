# Sync INCI

Sync INCI to projekt lokalnego narzędzia do przenoszenia informacji o składnikach kosmetyków z własnych ofert Allegro do katalogu produktów Base, a następnie do opisów ofert na ERLI.

## Cel aplikacji

Na Allegro składniki kosmetyków mogą znajdować się w osobnym polu, poza opisem oferty. W ofertach ERLI obsługiwanych przez właściciela aplikacji skład jest umieszczany w opisie. Narzędzie ma ograniczyć ręczne przepisywanie danych i pomyłki oraz zapewnić spójność informacji o produktach między platformami.

## Sposób działania

1. Odczyt składników INCI z ofert należących do autoryzowanego sprzedawcy Allegro.
2. Dopasowanie ofert do produktów w katalogu Base.
3. Uzupełnienie parametru `Składniki(INCI)` w odpowiednich produktach Base.
4. Umieszczenie składu w osobnej trzeciej sekcji dla ofert ERLI z dwiema sekcjami opisu, a w opisach z jedną sekcją — na końcu tej sekcji, zgodnie z wyborem właściciela.

Kolejność i treść składników mają być zachowywane zgodnie z danymi źródłowymi. Brakujące dane i niejednoznaczne dopasowania wymagają sprawdzenia przez właściciela aplikacji.

## Dostęp do Allegro

- Nazwa zarejestrowanej aplikacji: **Pobieranie INCI**.
- Wersja: **1.0**.
- Autoryzacja użytkownika: **OAuth 2.0 Device Flow**.
- Wymagany zakres: `allegro:api:sale:offers:read` — odczyt danych o ofertach.
- Aplikacja nie potrzebuje uprawnień do zmiany ofert Allegro ani dostępu do zamówień, płatności i wiadomości.
- Zapytania mają używać identyfikatora User-Agent wygenerowanego i sprawdzonego w oficjalnym narzędziu Allegro.

Adres informacji o aplikacji do generatora User-Agent:

https://github.com/magda13288/Sync-INCI

Identyfikator User-Agent aplikacji:

```text
Pobieranie-INCI/1.0 (+https://github.com/magda13288/Sync-INCI)
```

## Stan projektu i dane dostępowe

Dokumentacja znajduje się w folderze `doc`. [Układ folderów i instrukcja uruchamiania](STRUKTURA.md) opisują lokalne skrypty, konfigurację, dane, raporty i kopie.

Lokalne skrypty autoryzacji, pobierania składników z Allegro, uzupełniania parametru `Składniki(INCI)` w katalogu Base i dodawania składu do istniejących opisów ERLI są przygotowane. Zapis poprzedza raport dopasowań po SKU i EAN. Narzędzie uzupełnia puste parametry Base, zachowuje pozostałe parametry i kopię danych sprzed zmiany oraz potwierdza zapis ponownym odczytem. W ERLI zachowuje treść opisów i zdjęcia, wysyła wyłącznie zmieniony opis oraz weryfikuje pełny opis po zapisie. W ofertach z dwiema sekcjami tworzy trzecią sekcję z INCI; dokładny blok dopisany wcześniej do drugiej sekcji przenosi bez duplikowania składu. Brakujące składy, ręcznie zmienione bloki i sprzeczne dopasowania są pomijane i zgłaszane w lokalnym raporcie.

To publiczne repozytorium zawiera dokumentację aplikacji. Kod roboczy pozostaje na komputerze właściciela. Client Secret, tokeny Allegro oraz klucze API Base i ERLI nie są publikowane. Lokalne skrypty konfiguracji zapisują dane dostępowe przy użyciu Windows DPAPI, w postaci zaszyfrowanej dla konta Windows właściciela.

## Kontakt

Właściciel projektu: [magda13288 na GitHub](https://github.com/magda13288).

Pytania o cel i działanie aplikacji można zgłaszać w [Issues tego repozytorium](https://github.com/magda13288/Sync-INCI/issues). Nie należy umieszczać tam danych dostępowych ani tokenów.
