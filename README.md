# Sync INCI

Sync INCI to projekt lokalnego narzędzia do przenoszenia informacji o składnikach kosmetyków z własnych ofert Allegro do katalogu produktów Base, a następnie do opisów ofert na ERLI.

## Cel aplikacji

Na Allegro składniki kosmetyków mogą znajdować się w osobnym polu, poza opisem oferty. W ofertach ERLI obsługiwanych przez właściciela aplikacji skład jest umieszczany w opisie. Narzędzie ma ograniczyć ręczne przepisywanie danych i pomyłki oraz zapewnić spójność informacji o produktach między platformami.

## Planowany sposób działania

1. Odczyt składników INCI z ofert należących do autoryzowanego sprzedawcy Allegro.
2. Dopasowanie ofert do produktów w katalogu Base.
3. Uzupełnienie parametru `Składniki(INCI)` w odpowiednich produktach Base.
4. Wykorzystanie składu na końcu drugiej sekcji opisu oferty ERLI.

Kolejność i treść składników mają być zachowywane zgodnie z danymi źródłowymi. Brakujące dane i niejednoznaczne dopasowania wymagają sprawdzenia przez właściciela aplikacji.

## Dostęp do Allegro

- Nazwa zarejestrowanej aplikacji: **Pobieranie INCI**.
- Wersja: **1.0.0**.
- Autoryzacja użytkownika: **OAuth 2.0 Device Flow**.
- Wymagany zakres: `allegro:api:sale:offers:read` — odczyt danych o ofertach.
- Aplikacja nie potrzebuje uprawnień do zmiany ofert Allegro ani dostępu do zamówień, płatności i wiadomości.
- Zapytania mają używać identyfikatora User-Agent wygenerowanego i sprawdzonego w oficjalnym narzędziu Allegro.

Adres informacji o aplikacji do generatora User-Agent:

https://github.com/magda13288/Sync-INCI

## Stan projektu i dane dostępowe

Projekt jest w trakcie przygotowania. Lokalny skrypt autoryzacji jest przygotowany; pobieranie składników i aktualizacja katalogu Base nie są jeszcze wdrożone.

To publiczne repozytorium zawiera dokumentację aplikacji. Kod roboczy pozostaje na komputerze właściciela. Client Secret, tokeny Allegro i klucz API Base nie są publikowane. Lokalny skrypt autoryzacji zapisuje dane dostępowe przy użyciu Windows DPAPI, w postaci zaszyfrowanej dla konta Windows właściciela.

## Kontakt

Właściciel projektu: [magda13288 na GitHub](https://github.com/magda13288).

Pytania o cel i działanie aplikacji można zgłaszać w [Issues tego repozytorium](https://github.com/magda13288/Sync-INCI/issues). Nie należy umieszczać tam danych dostępowych ani tokenów.
