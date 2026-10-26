# Paliwo na trasę

Kalkulator planu żywienia i nawodnienia na wyjazd rowerowy. Na podstawie trasy (także z pliku GPX), zawodnika, roweru, opon i pogody liczy wydatek energii, potrzebne węglowodany, płyny i sód, a potem rozpisuje wybrane produkty (żele, batony, jedzenie, napoje, elektrolity) na czas i kilometry.

Cała aplikacja to jedna statyczna strona: `index.html` plus pliki z danymi. Nie potrzebuje serwera aplikacyjnego ani bazy danych.

## Pliki

| Plik | Zawartość |
|---|---|
| `index.html` | aplikacja |
| `produkty.csv` | żele, żelki, batony, jedzenie, kapsułki z solą, napoje do bidonów, elektrolity |
| `opony.csv` | opony i ich opór toczenia (Crr) |
| `miejscowosci.csv` | miejscowości do opisu profilu trasy (GeoNames, CC BY 4.0) |

Pliki CSV używają średnika jako separatora i otwierają się bezpośrednio w Excelu. Liczby mogą mieć przecinek albo kropkę dziesiętną. Po edycji zapisz plik jako CSV (UTF-8).

### `produkty.csv`

| kolumna | opis |
|---|---|
| `lista` | `produkt`, `napoj` albo `elektrolity` |
| `id` | krótki, unikalny identyfikator bez spacji; nie zmieniaj go w istniejących pozycjach (przeglądarki użytkowników zapamiętują po nim zaznaczenia) |
| `nazwa` | nazwa widoczna na stronie |
| `rodzaj` | tylko dla `produkt`: `zel`, `zelki`, `baton`, `jedzenie`, `sol` |
| `wegle_g`, `kcal`, `sod_mg`, `kofeina_mg` | wartości na sztukę, a dla napojów na porcję |
| `zrodlo_cukru` | `mieszanka` (glukoza + fruktoza) albo `glukoza` |
| `plyn_ml` | opcjonalnie, np. 330 dla puszki coli |

### `opony.csv`

| kolumna | opis |
|---|---|
| `kategoria` | grupa na liście. Kategorie zaczynające się od „Szosa” są liczone jako wąskie opony szosowe, pozostałe jako szerokie (mniejsze straty na szutrze) |
| `id` | unikalny identyfikator bez spacji |
| `nazwa` | nazwa widoczna na stronie |
| `crr` | współczynnik oporu toczenia z pomiaru na rolce, np. `0.0029` |

## Uruchomienie

Strona wczytuje pliki CSV przez `fetch`, więc musi być serwowana przez HTTP(S). Otwarcie `index.html` podwójnym kliknięciem z dysku nie zadziała.

- **GitHub Pages:** Settings → Pages → Source: *Deploy from a branch*, gałąź `main`, folder `/ (root)`. Strona będzie pod adresem `https://wroobel.github.io/FeedMeApp/`.
- **Lokalnie:** `python3 -m http.server` w tym folderze, potem http://localhost:8000.

Przycisk „Pobierz prognozę” korzysta z darmowego API Open-Meteo i działa na zwykłym hostingu.

## Uwagi

Wartości produktów i opór toczenia opon są przybliżone. Kalkulator to narzędzie planistyczne, nie porada medyczna.
