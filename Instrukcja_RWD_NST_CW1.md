# Responsive Web Design (NST), zajęcia 1: diagnoza strony w DevTools

**Link do raportu w  MS Forms:** https://forms.cloud.microsoft/e/fYB54ttUxf

Strona festiwalu „Retrotechnika 2026” ma kilka ukrytych usterek. Znajdujesz je narzędziami przeglądarki i wybierasz w formularzu **konkretne wartości** (liczby, nazwy, kolory). Te same usterki sprawdzam w projektach zaliczeniowych, więc to zadanie jest też treningiem przed oceną projektu.

## Ściąga

| Co | Jak |
|---|---|
| Otwórz DevTools | `F12` albo `Ctrl+Shift+I` , w przeglądarkach innych niż Chrome skróty i nazwy mogą być inne (np. Inspektor) |
| Wskaż element na stronie | `Ctrl+Shift+C`, potem kliknij element |
| Szukaj w kodzie (Elements) | kliknij w panel Elements, `Ctrl+F` |
| Odśwież bez pamięci podręcznej | `Ctrl+Shift+R` |

**Zakładki DevTools:** Elements (kod i style), Console (błędy skryptów), Network (pobrane pliki), Lighthouse (automatyczny test). Gdy zakładki nie widać, kliknij `>>`.

Wybierasz odpowiedź **dokładnie taką, jaką pokazuje DevTools** (bez zaokrąglania). Warianty mają te same opcje odpowiedzi, ale inne wartości: odpowiedzi z sąsiedniego komputera mogą być złe. Formularz otwórz w zwykłym oknie, stronę w **oknie incognito** (`Ctrl+Shift+N`), bo dodatki przeglądarki psują wyniki.

---

## Część 0. Start

1. Otwórz formularz **swojego wariantu** i wpisz numer albumu.
2. W oknie incognito otwórz stronę swojego wariantu. Naciśnij `F12`.

## Część 1. Tryb telefonu i szerokości ekranu

1. `Ctrl+Shift+M`. Na pasku nad stroną wybierz **Dimensions: Responsive**, w polu szerokości wpisz **360**, Enter.
2. Przewiń stronę w bok. Strona „ucieka” w prawo: jakiś element jest szerszy niż ekran.
3. `Ctrl+Shift+C` i kliknij szary pasek z listą partnerów. W panelu Elements zobaczysz zaznaczony znacznik.
   * **Pytanie 1.** Jaką **klasę** ma element, który rozpycha stronę?
4. Przy zaznaczonym elemencie przejdź w prawym panelu do zakładki **Computed** i odczytaj `width`.
   * **Pytanie 2.** Ile pikseli ma szerokość tego elementu?
5. Spójrz na górę strony przy 360 px: czerwona plakietka zasłania nagłówek. Zaznacz ją `Ctrl+Shift+C`.
   * **Pytanie 3.** Jaką klasę ma element, który zasłania nagłówek `h1`?
6. Zmieniaj szerokość, przeciągając prawą krawędź ramki (albo wpisując liczby): 700, 760, 800, 1000. Obserwuj menu: przy małej szerokości jest ikona „hamburgera”, przy dużej linki są w jednym rzędzie.
   * **Pytanie 4.** Od jakiej szerokości (px) menu wyświetla się w poziomie? Podpowiedź: kliknij `<nav>` w Elements i poszukaj w klasie fragmentu `navbar-expand-…`. Bootstrap: `sm` = 576, `md` = 768, `lg` = 992, `xl` = 1200.

## Część 2. Elements i Computed: przycisk, kolor, krój

1. Wróć do 360 px. W sekcji z nagłówkiem jest żółty przycisk z ołówkiem ✎. Najedź na niego `Ctrl+Shift+C`: dymek pokazuje wymiary, np. `a.btn 50 × 50`.
   * **Pytanie 5.** Jakie wymiary (szerokość x wysokość) ma przycisk?
   * Minimalny wygodny obszar dotyku to 44 × 44 px. Ten przycisk jest za mały.
2. Zaznacz tekst w stopce (na samym dole strony). W panelu **Styles** znajdź regułę `.stopka` i właściwość `color`.
   * **Pytanie 6.** Jaki kolor (HEX, np. `#123456`) ma tekst stopki?
3. Kliknij mały kwadracik koloru obok wartości `color`. Otworzy się próbnik koloru z linią **Contrast ratio**.
   * **Pytanie 7.** Jaki współczynnik kontrastu pokazuje DevTools (liczba, np. `3.15`)? Wymóg WCAG dla zwykłego tekstu: co najmniej 4.5.
4. Zaznacz nagłówek `h1`. W zakładce **Computed** przewiń na sam dół do sekcji **Rendered Fonts**.
   * **Pytanie 8.** Jakim krojem przeglądarka **faktycznie** wyświetla nagłówek? (W Styles zobaczysz, jaki krój zadeklarowano: porównaj.)

## Część 3. Console i Network

1. Kliknij zakładkę **Console**. Czerwony wiersz to błąd skryptu.
   * **Pytanie 9.** Jak nazywa się funkcja, której brakuje (`… is not defined`)?
2. Kliknij **Network**, odśwież stronę `Ctrl+Shift+R`. Czerwone wiersze to pliki, których serwer nie znalazł (status 404).
   * **Pytanie 10.** Którego **obrazka** brakuje? (Wśród czerwonych wierszy jest też plik fontu: to wyjaśnia odpowiedź na pytanie 8.)
3. Zamknij tryb telefonu (`Ctrl+Shift+M`). Kliknij po kolei każdą pozycję w menu.
   * **Pytanie 11.** Która pozycja menu prowadzi do strony błędu 404?

## Część 4. SEO i obrazki

1. W Elements naciśnij `Ctrl+F` i wpisz `ld+json`. Znajdziesz blok danych strukturalnych schema.org.
   * **Pytanie 12.** Jaka data jest w polu `startDate`?
2. Skopiuj zawartość tego bloku (bez znaczników `<script>`), wejdź na **validator.schema.org**, zakładka **Code snippet**, wklej i kliknij **Run test**.
   * **Pytanie 13.** Co pokazuje walidator? (Podpowiedź: spójrz na przecinek przed ostatnim nawiasem `}`.)
3. W Elements `Ctrl+F`, wpisz selektor `img:not([alt])` (obrazek bez atrybutu `alt`). Obok pola wyszukiwania pojawi się licznik, np. `1 of 4`.
   * **Pytanie 14.** Ile znaczników `<img>` **nie ma** atrybutu `alt`?

## Część 5. Lighthouse

1. Zakładka **Lighthouse**: Mode **Snapshot**, Device **Mobile**, zaznacz tylko **Accessibility**. Kliknij **Analyze page load** i poczekaj (do 2 minut).
2. Przewiń raport do listy problemów oznaczonych czerwonym trójkątem.
   * **Pytanie 15.** Które problemy zgłosił Lighthouse?

Kliknij **Prześlij** dopiero po pytaniu 15.

---

### Co z tego wynika dla projektu

Każde pytanie odpowiada jednemu kryterium oceny projektu: przewijanie poziome (1–2), nachodzenie elementów (3), menu (4), przyciski 44 × 44 (5), kontrast (6–7), fonty z karty (8), działające linki (10–11), schema.org (12–13), opisy obrazków (14). Przed oddaniem projektu sprawdzasz swoją stronę tymi samymi narzędziami.
