# Analiza merytoryczna instrukcji technicznych

> **Status:** OSTATECZNY / AKTUALNY  
> **Wersja:** 2.0  
> **Przeznaczenie:** Publiczny standard pracy agenta modernizującego instrukcje Confluence  
> **Bezpieczeństwo:** Dokument nie zawiera danych organizacyjnych ani danych dostępowych  
> **Zasada nadrzędna:** Materiały bieżącego zadania mają pierwszeństwo przed neutralnymi przykładami.

## Cel

Analiza służy wykrywaniu niespójności logicznych, proceduralnych i technicznych. Nie daje zgody na automatyczne poprawianie danych technicznych. Raport pozostaje poza treścią Confluence do czasu decyzji użytkownika.

## Źródła

Podstawą są materiały bieżącego zadania:

1. aktualny JSON strony;
2. aktualny PDF, tekst lub zrzuty;
3. dokumentacja konkretnego wdrożenia;
4. decyzje użytkownika.

Oficjalna dokumentacja produktu opisuje działanie ogólne. Nie potwierdza konfiguracji środowiska użytkownika. Przy rozbieżności zachowaj dane z aktualnej instrukcji, pokaż konflikt i poczekaj na decyzję.

## Inwentaryzacja

Przed oceną zidentyfikuj:

- rozdziały i kroki;
- moduły, usługi i procesy;
- hosty i środowiska;
- konta i wymagane uprawnienia;
- komendy, argumenty i placeholdery;
- ścieżki, pliki, URL i porty;
- logi, monitoring i alarmy;
- oczekiwane wyniki i wartości kontrolne.

## Kontrole

### Nazewnictwo

Porównaj nazwy w tabelach, opisach, nagłówkach i komendach. Wykrywaj różnice w prefiksach, myślnikach, podkreśleniach, wielkości liter oraz końcówkach `.service` i `.target`.

### Hosty i środowiska

Sprawdź, czy hosty są konsekwentnie przypisane do środowisk, nie występują w sprzecznych grupach i są zgodne pomiędzy tabelą a tekstem. Nie wyprowadzaj środowiska tylko z nazwy hosta.

### Konta i uprawnienia

Sprawdź konto wykonujące każdą czynność, użycie `sudo`, wymagane przełączenie użytkownika oraz różnicę pomiędzy usługą systemową i usługą użytkownika.

### Komendy

Dla każdej komendy ustal działanie, usługę lub proces, konto, środowisko, zależność od poprzedniego kroku i oczekiwany wynik. Porównaj `start`, `stop`, `status` i `restart`. Sprawdź pełne ścieżki, przekierowania, placeholdery i potencjalne uszkodzenia przez automatyczne linki.

Nie wykonuj komend. Oceniaj spójność dokumentu.

### Kolejność procedury

Sprawdź, czy:

1. logowanie lub zmiana konta następują przed komendą;
2. zatrzymanie następuje przed czynnością wymagającą zatrzymania;
3. uruchomienie następuje po zmianie lub czyszczeniu;
4. weryfikacja następuje po uruchomieniu;
5. plik jest pobrany przed analizą;
6. porównywane wartości zostały wcześniej uzyskane;
7. późniejszy krok nie wymaga brakujących danych.

### Wymagania wstępne

Sprawdź dostęp do hosta, repozytorium, monitoringu, wymagane konto, katalog roboczy, narzędzia, dane wejściowe oraz okno serwisowe. Zgłaszaj tylko braki istotne dla konkretnej procedury.

### Rezultat i weryfikacja

Sprawdź obecność kontroli statusu, logów, alarmów, procesu, aplikacji, plików błędów, pakietów lub wyniku komendy. Brak kontroli po operacji o istotnym wpływie zgłoś jako brak albo sugestię.

### Logi i monitoring

Porównaj ścieżki logów w tabeli i tekście. Sprawdź kontekst ścieżek względnych, konto wymagane do odczytu oraz zgodność pliku logu z przekierowaniem.

Dla monitoringu wskaż dokładnie host, element, alarm, wykres, zakres czasu oraz potrzebny zrzut lub link. Nie twierdź, że monitoring został sprawdzony bez danych.

### Tabela i opis

Porównaj moduły, hosty, środowiska, konta, usługi, komendy, logi, sposób restartu, wyjątki i weryfikację.

### Przykłady

Sprawdź zgodność nazwy, wersji, składni i formatu wyniku. Nie aktualizuj przykładowych wartości bez decyzji użytkownika.

## Klasyfikacja

### Błąd krytyczny

Problem mogący prowadzić do działania na złym środowisku, błędnej komendy, utraty danych, istotnej niedostępności, pominięcia zabezpieczenia lub publikacji na niewłaściwej stronie. Nierozwiązany błąd krytyczny blokuje `PUBLISH`.

### Sprzeczność

Dwa fragmenty podają różne informacje o tym samym elemencie.

### Brak

Nie ma informacji potrzebnej do jednoznacznego wykonania konkretnego kroku.

### Niejasność

Treść ma kilka możliwych interpretacji albo wymaga potwierdzenia.

### Sugestia

Zmiana poprawiająca użyteczność, która nie wynika z potwierdzonego błędu.

## Wpływ i pewność

Wpływ:

- **Wysoki** — ryzyko błędnej operacji, utraty danych lub istotnej niedostępności;
- **Średni** — ryzyko pominięcia kontroli lub błędnej interpretacji;
- **Niski** — problem precyzji lub czytelności.

Pewność:

- **Potwierdzony** — wynika bezpośrednio z materiałów;
- **Prawdopodobny** — wynika z logicznego porównania;
- **Do weryfikacji** — brakuje danych.

## Raport

Podziel wynik na:

1. Błędy krytyczne;
2. Sprzeczności;
3. Braki;
4. Niejasności;
5. Sugestie;
6. Brakujące materiały;
7. Kontrole niewykonane.

Dla każdego problemu podaj:

```text
Identyfikator:
Kategoria:
Wpływ:
Pewność:
Lokalizacja:
Fragment źródłowy 1:
Fragment źródłowy 2:
Opis problemu:
Możliwy wpływ:
Proponowana decyzja:
Dane potrzebne do weryfikacji:
```

Przy braku problemów napisz:

```text
Nie wykryto sprzeczności merytorycznych na podstawie dostępnych materiałów.
```

Następnie wymień wykorzystane źródła i ograniczenia.

## Zakaz automatycznej publikacji raportu

Raportu nie wolno automatycznie dodawać do `body.storage.value`, makra, komentarza wersji ani strony testowej lub docelowej. Zastosowanie poprawki wymaga decyzji użytkownika.

---

## Powiązane moduły

- [Strona główna standardu](index.html)
- [Analiza merytoryczna](analiza-merytoryczna.html)
- [Standard wizualny](standard-wizualny.html)
- [Format Confluence](format-confluence.html)
- [Code review](code-review.html)
- [Znane błędy](znane-bledy.html)

## Macierz spójności usług

Dla każdego modułu przygotuj roboczą macierz obejmującą:

- nazwę modułu;
- środowisko;
- hosty;
- konto;
- start;
- stop;
- status;
- restart;
- logi;
- kontrolę po operacji.

Macierz służy wyłącznie analizie. Nie publikuj jej automatycznie w Confluence. Różne wartości w jednym wierszu są kandydatem do raportu, a nie zgodą na zmianę.

## Analiza procedury awaryjnej i odwracalności

Dla operacji wpływających na dostępność sprawdź, czy materiał określa:

- warunek rozpoczęcia;
- warunek przerwania;
- sposób oceny powodzenia;
- działanie po niepowodzeniu;
- możliwość cofnięcia;
- źródło danych potrzebnych do cofnięcia;
- osobę lub rolę podejmującą decyzję, jeśli informacja występuje w źródle.

Brak procedury cofnięcia nie zawsze jest błędem. Klasyfikuj według wpływu i zakresu instrukcji.

## Aktualność wiedzy produktowej

Przy użyciu dokumentacji publicznej zapisz:

- nazwę produktu;
- wersję dokumentacji;
- datę dostępu;
- adres oficjalnego źródła;
- zakres informacji wykorzystany w analizie.

Nie stosuj instrukcji dla innej wersji produktu bez oznaczenia różnicy. Jeżeli wersja wdrożenia jest nieznana, oznacz wniosek jako wymagający potwierdzenia.

## Pytania decyzyjne

Pytanie do użytkownika ma:

- dotyczyć jednego konfliktu;
- wskazywać dokładne warianty;
- opisywać wpływ wyboru;
- nie sugerować, że jeden wariant został już zatwierdzony;
- umożliwiać odpowiedź krótką i jednoznaczną.

Przykład neutralny:

```text
W rozdziale 4 występuje example-a.service, a w tabeli example-b.service.
Która nazwa ma zostać użyta w wersji testowej: A, B czy pozostawienie źródła bez zmiany?
```

## Blokada i zakres kontynuacji

Nierozwiązany problem może blokować tylko część procesu. Agent może nadal przygotować analizę, podgląd struktury i listę braków, lecz nie może przedstawiać niezweryfikowanej treści jako gotowej do publikacji. PUBLISH blokują w szczególności konflikty wysokiego wpływu dotyczące hosta, środowiska, usługi, konta, komendy, danych dostępowych lub strony docelowej.

## Kontrola regresyjna analizy

Po decyzjach użytkownika ponownie sprawdź:

1. czy rozwiązano wskazany konflikt;
2. czy zmiana nie stworzyła nowej sprzeczności;
3. czy decyzja nie została zastosowana szerzej niż polecono;
4. czy raport i treść strony nadal są rozdzielone;
5. czy problemy nierozwiązane zachowały właściwy status.
