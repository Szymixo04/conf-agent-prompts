# Analiza merytoryczna instrukcji technicznych

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
