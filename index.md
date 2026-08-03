# Standard agenta modernizacji instrukcji Confluence

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
