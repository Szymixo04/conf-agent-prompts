# Code review skryptów modernizujących Confluence

> **Status:** OSTATECZNY / AKTUALNY  
> **Wersja:** 2.0  
> **Przeznaczenie:** Publiczny standard pracy agenta modernizującego instrukcje Confluence  
> **Bezpieczeństwo:** Dokument nie zawiera danych organizacyjnych ani danych dostępowych  
> **Zasada nadrzędna:** Materiały bieżącego zadania mają pierwszeństwo przed neutralnymi przykładami.

## Cel

Skrypt nie może zostać przekazany jako sprawdzony bez rzeczywistego wykonania dostępnych kontroli. Po każdej poprawce powtórz kontrole zależne od zmienionego fragmentu oraz końcowy zestaw regresyjny.

## 1. Kontrola składni JavaScript

Wykonaj parser lub `node --check` na zapisanym pliku.

Sprawdź:

- nawiasy i klamry;
- cudzysłowy i apostrofy;
- template strings;
- backslashe;
- wyrażenia regularne;
- funkcje asynchroniczne;
- nazwy zmiennych;
- brak fragmentów HTML wklejonych do kodu;
- prawidłowe zakończenie wywołania i obsługę błędów.

Samo przeczytanie kodu nie jest kontrolą składni.

## 2. Identyfikatory i tryby

Rozróżniaj:

```text
SOURCE_PAGE_ID
TEST_PAGE_ID
TARGET_PAGE_ID
```

Domyślny tryb to `TEST`. W trybie TEST adres PUT i pobrana strona muszą wskazywać stronę testową. `TARGET_PAGE_ID` nie może zostać użyty w żądaniu aktualizacyjnym.

`PUBLISH` wymaga jawnej decyzji użytkownika oraz świeżego odczytu strony docelowej.

## 3. REST API

Sprawdź:

- poprawny endpoint;
- metodę GET przed PUT;
- `credentials: "same-origin"` dla skryptu wykonywanego w zalogowanej karcie;
- nagłówki `Accept` i `Content-Type`;
- obsługę błędów HTTP;
- parsowanie odpowiedzi JSON;
- brak tokenów i haseł w kodzie;
- body wysyłane przez `JSON.stringify`.

Nie zakładaj, że brak wyjątku oznacza poprawny zapis.

## 4. Kopia bezpieczeństwa

Przed PUT pobierz i zapisz:

- datę;
- id i typ;
- tytuł;
- wersję;
- space;
- ancestors;
- bezpośredniego rodzica;
- `body.storage`;
- aktywny tryb i role identyfikatorów.

Kopia musi powstać przed aktualizacją.

## 5. Wersjonowanie

Nowa wersja ma wynosić:

```text
currentPage.version.number + 1
```

Nie używaj wersji zapisanej na stałe. Bezpośrednio przed PUBLISH pobierz świeżą wersję strony. Przy konflikcie przerwij.

Komentarz wersji:

```javascript
message: ""
```

## 6. Tytuł i położenie

Zachowaj tytuł, przestrzeń i bezpośredniego rodzica. Jeżeli nie można ustalić rodzica, przerwij zamiast podstawiać identyfikator.

Po zapisie porównaj rodzica z wartością sprzed aktualizacji.

## 7. Storage Format

Wykonaj walidację XML/XHTML zgodnie z modułem Format Confluence.

Sprawdź:

- domknięcie znaczników;
- makra;
- parametry;
- CDATA;
- encje;
- tabele;
- brak przypadkowych elementów `a` w komendach.

## 8. Kompletność

Przed transformacją utwórz trwałą listę kontrolną:

- główne nagłówki;
- moduły;
- hosty;
- usługi;
- konta;
- komendy;
- ścieżki;
- URL;
- wersje;
- znaczące wartości;
- tytuły wymaganych makr i bloków.

Po transformacji sprawdź każdy element semantycznie.

Nie dodawaj do listy kontrolnej dokładnego HTML, stylów ani wariantu `<br/>`.

## 9. Tabele

Sprawdź:

- liczbę kolumn;
- nagłówki;
- liczbę wierszy;
- listę modułów;
- hosty przed i po grupowaniu;
- konta;
- komendy;
- ścieżki logów;
- brak utraty kolumny logów.

Kontrola wizualna wymaga rzeczywistego podglądu strony. Jeżeli nie wykonano podglądu, zaznacz ograniczenie.

## 10. Długie komendy

Porównaj komendę przed i po podziale. Sprawdź, czy nie rozdzielono hosta, ścieżki, URL, nazwy usługi lub operatora przekierowania. Nie dodawaj argumentów nieobecnych w źródle.

## 11. Walidacja po PUT

Po aktualizacji wykonaj ponowny GET. Sprawdź:

- id;
- numer wersji;
- tytuł;
- rodzica;
- parsowalność Storage Format;
- trwałe dane z listy kontrolnej.

Nie uznawaj normalizacji HTML za utratę informacji.

## 12. Błąd po zapisie

Jeżeli PUT mógł się udać, ale walidacja zgłosiła błąd:

1. nie wykonuj kolejnego PUT;
2. pobierz stronę ponownie;
3. ustal faktyczny numer wersji;
4. oddziel błąd zapisu od błędu walidatora;
5. popraw walidator, jeśli treść została zachowana.

## 13. Testy regresyjne

Końcowa kontrola powinna obejmować:

- składnię JavaScript;
- właściwy tryb i pageId;
- pusty komentarz wersji;
- kopię bezpieczeństwa;
- zachowanie rodzica;
- poprawny XML;
- kompletność trwałych danych;
- brak przypadkowych linków;
- ponowny GET po zapisie.

## 14. Raport

Podaj:

- nazwę pliku;
- tryb;
- pageId zmienianej strony;
- wpływ na stronę docelową;
- wykonane testy i ich wyniki;
- testy niewykonane;
- ograniczenia;
- sumę kontrolną pliku.

Nie deklaruj wyniku kontroli, której nie wykonano.

---

## Powiązane moduły

- [Strona główna standardu](index.html)
- [Analiza merytoryczna](analiza-merytoryczna.html)
- [Standard wizualny](standard-wizualny.html)
- [Format Confluence](format-confluence.html)
- [Code review](code-review.html)
- [Znane błędy](znane-bledy.html)

## Kolejność bramek jakości

Skrypt przechodzi kolejno:

1. **Brama wejścia** — kompletność i integralność JSON/PDF.
2. **Brama transformacji** — zachowanie danych chronionych.
3. **Brama składni** — parser JavaScript.
4. **Brama Storage Format** — XML, makra, CDATA i tabele.
5. **Brama trybu** — identyfikatory oraz blokada PUBLISH.
6. **Brama przed PUT** — kopia, świeża wersja i payload.
7. **Brama po PUT** — ponowny GET i walidacja semantyczna.
8. **Brama wizualna** — rzeczywisty podgląd strony testowej.

Nie przechodź do kolejnej bramy po błędzie blokującym.

## Statyczne testy obowiązkowe

Jeżeli środowisko umożliwia wykonanie kodu, zapisz skrypt do pliku i uruchom rzeczywisty parser. Dodatkowo wyszukaj:

- twardo zapisane numery wersji;
- więcej niż jedno żądanie PUT;
- PUT przed kopią lub walidacją;
- nieużywane TARGET_PAGE_ID w TEST;
- tokeny, nagłówki Authorization i ciasteczka;
- `eval`, `Function` i niepotrzebne wykonywanie tekstu;
- automatyczny retry aktualizacji;
- `message` inne niż pusty ciąg.

## Testy funkcji pomocniczych

Oddzielnie testuj:

- kodowanie XML;
- przygotowanie CDATA;
- grupowanie hostów;
- podział długiej komendy;
- normalizację tekstu;
- porównanie list chronionych elementów;
- budowę nazwy kopii;
- wyznaczenie bezpośredniego rodzica.

Do testów używaj neutralnych danych zawierających cudzysłowy, apostrofy, ampersand, polskie znaki, URL, placeholder oraz backslash.

## Brama przed PUT

Bezpośrednio przed PUT sprawdź i wyświetl:

- aktywny tryb;
- id pobranej strony;
- id w endpointcie;
- tytuł;
- wersję bieżącą i planowaną;
- rodzica;
- wynik kopii;
- wynik XML;
- liczbę brakujących elementów chronionych.

PUT jest dozwolony wyłącznie, gdy liczba brakujących elementów wynosi zero i nie ma błędu blokującego.

## Kontrola odpowiedzi HTTP

Zapisz kod HTTP i czytelną treść błędu. Obsłuż odpowiedź, która nie jest poprawnym JSON-em. Nie ujawniaj w raporcie ciasteczek ani wrażliwych nagłówków.

## Kontrola skutków

Po PUT nie opieraj sukcesu na odpowiedzi aktualizacyjnej. Wykonaj GET ze świeżym parametrem czasu lub właściwymi nagłówkami, jeżeli cache może zakłócić wynik. Potwierdź numer wersji, tytuł, rodzica i treść.

## Klasyfikacja wyników testów

Każdy test oznacz jako:

- `PASS` — wykonany i pozytywny;
- `FAIL` — wykonany i negatywny;
- `NOT RUN` — niewykonany;
- `BLOCKED` — niemożliwy z powodu brakujących danych lub narzędzia;
- `MANUAL` — wymaga podglądu lub decyzji użytkownika.

Nie zamieniaj `NOT RUN` na `PASS` na podstawie inspekcji wzrokowej.

## Minimalny raport końcowy

Raport musi identyfikować plik przez nazwę i SHA-256, wskazywać tryb, identyfikatory, wynik każdej bramy, dokładny pageId możliwy do zmiany oraz informację, czy PUT jest aktywny. Przy TEST wyraźnie potwierdź, że TARGET_PAGE_ID nie jest używany do aktualizacji.
