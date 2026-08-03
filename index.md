# Standard agenta modernizacji instrukcji Confluence

> **Status:** OSTATECZNY / AKTUALNY  
> **Wersja:** 2.0  
> **Przeznaczenie:** Publiczny standard pracy agenta modernizującego instrukcje Confluence  
> **Bezpieczeństwo:** Dokument nie zawiera danych organizacyjnych ani danych dostępowych  
> **Zasada nadrzędna:** Materiały bieżącego zadania mają pierwszeństwo przed neutralnymi przykładami.


## Przeznaczenie

Ta witryna zawiera publiczne i neutralne standardy pracy agenta analizującego, modernizującego i kontrolującego instrukcje techniczne w Confluence.

Materiały określają **metodykę działania**, a nie rzeczywiste dane konkretnego środowiska. Nie wolno umieszczać tutaj prawdziwych hostów, wewnętrznych adresów, kont technicznych, dokumentacji operacyjnej, haseł, tokenów, plików JSON stron ani innych danych organizacyjnych.

## Moduły

- [Analiza merytoryczna](analiza-merytoryczna.html)
- [Standard wizualny](standard-wizualny.html)
- [Format Confluence](format-confluence.html)
- [Code review](code-review.html)
- [Znane błędy](znane-bledy.html)

## Hierarchia źródeł

Agent stosuje następującą kolejność:

1. Jednoznaczna decyzja użytkownika w bieżącej rozmowie.
2. Aktualny JSON, PDF, tekst i zrzuty przekazane w bieżącym zadaniu.
3. Standardy opisane w tej witrynie.
4. Oficjalna dokumentacja produktu lub projektu.
5. Neutralne przykłady przedstawione w tej witrynie.

Aktualny JSON strony jest nadrzędnym źródłem rzeczywistych:

- komend;
- nazw usług;
- hostów;
- kont;
- ścieżek;
- parametrów;
- wartości;
- wersji;
- numeracji;
- kolejności czynności.

Neutralnych przykładów z tej witryny nie wolno kopiować jako danych rzeczywistego środowiska.

## Dobór modułów

Dla standardowej modernizacji użyj:

1. analizy merytorycznej;
2. standardu wizualnego;
3. code review.

Moduł **Format Confluence** jest obowiązkowy podczas generowania lub kontroli `body.storage.value`.

Moduł **Znane błędy** jest obowiązkowy, gdy wystąpił błąd wykonania, nieoczekiwana normalizacja HTML, fałszywy błąd walidacji, automatyczny link w kodzie albo problem z szerokością tabeli.

Nie pobieraj wszystkich modułów bez potrzeby.

## Wiedza o produktach i systemach

Ta witryna nie jest dokumentacją konkretnych systemów.

Wiedzę o konkretnym wdrożeniu agent otrzymuje od użytkownika w bieżącej rozmowie. Dla publicznie udokumentowanego produktu agent może używać aktualnej dokumentacji oficjalnej, ale nie może przedstawiać ustawień domyślnych produktu jako potwierdzonej konfiguracji środowiska użytkownika.

Agent nie może na podstawie Internetu wymyślać:

- wewnętrznych hostów;
- kont technicznych;
- nazw usług charakterystycznych dla wdrożenia;
- ścieżek;
- portów;
- alarmów;
- konfiguracji środowiskowej.

## Ochrona treści

Bez decyzji użytkownika agent nie zmienia:

- komend;
- hostów;
- usług;
- kont;
- ścieżek;
- parametrów;
- wartości;
- wersji;
- kolejności działań;
- numeracji głównych rozdziałów.

Wykryte problemy przedstawia poza treścią przeznaczoną do Confluence.

## Tryb pracy

Domyślnym trybem jest `TEST`.

Strona docelowa nie może zostać zmieniona bez jednoznacznej decyzji użytkownika. Akceptacja raportu albo wyglądu strony testowej nie oznacza automatycznej zgody na publikację.


---

## Status wydania

Wersja `1.0` jest pierwszą oficjalną wersją standardu przeznaczoną do testów agenta. Zmiany w kolejnych wersjach powinny wynikać z udokumentowanych błędów lub braków wykrytych w testach.

## Kontrakt działania agenta

Agent korzysta z tej bazy jako zestawu specjalistycznych checklist. Baza nie zastępuje instrukcji wbudowanej w agenta ani materiałów bieżącego zadania. Agent ma dobierać moduły do problemu, a nie pobierać wszystkie strony zapobiegawczo.

### Standardowa modernizacja istniejącej instrukcji

1. Odczytaj materiały użytkownika.
2. Zastosuj moduł Analiza merytoryczna.
3. Przedstaw osobny raport i poczekaj na decyzje dotyczące problemów technicznych.
4. Zastosuj Standard wizualny.
5. Wygeneruj treść zgodnie z Format Confluence.
6. Zastosuj Code review.
7. Przy błędzie skorzystaj ze Znanych błędów.
8. Domyślnie przygotuj TEST, nie PUBLISH.

### Tworzenie nowej instrukcji

1. Ustal publicznie udokumentowane działanie produktu z oficjalnych źródeł.
2. Oddziel wiedzę produktową od danych konkretnego wdrożenia.
3. Przygotuj listę brakujących danych środowiskowych.
4. Nie wstawiaj domyślnych hostów, kont ani ścieżek jako wartości rzeczywistych.
5. Przygotuj strukturę i wersję roboczą.
6. Zastosuj wszystkie właściwe kontrole przed TEST.

## Kryteria jakości odpowiedzi

Odpowiedź agenta powinna być audytowalna: wskazywać źródła, decyzje użytkownika, wykonane testy, kontrole niewykonane, ograniczenia oraz stronę, którą może zmienić skrypt. Samo stwierdzenie „sprawdzono” bez wymienienia kontroli jest niewystarczające.

## Zarządzanie zmianami standardu

Nową regułę dodawaj tylko wtedy, gdy:

- wykryto powtarzalny błąd;
- reguła nie dubluje istniejącej;
- wskazano moduł odpowiedzialny za regułę;
- przygotowano test regresyjny;
- neutralny przykład nie zawiera danych organizacyjnych.

Zmiana treści modułu wymaga podniesienia wersji i ponownego zgłoszenia zmienionych adresów do indeksacji.
