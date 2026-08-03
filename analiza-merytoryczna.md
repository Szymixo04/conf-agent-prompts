# Analiza merytoryczna instrukcji technicznych

## Cel modułu

Moduł określa sposób sprawdzania logicznej, proceduralnej i technicznej spójności instrukcji.

Analiza merytoryczna ma wykrywać problemy i przedstawiać je użytkownikowi. Nie jest zgodą na automatyczne poprawianie danych technicznych.

Raport analizy nie może zostać automatycznie dodany do treści Confluence, komentarza wersji ani skryptu publikującego.

---

## Źródła analizy

Podstawowym źródłem danych konkretnej instrukcji są materiały przekazane w bieżącej rozmowie:

1. aktualny JSON strony Confluence;
2. aktualny PDF instrukcji;
3. tekst lub zrzuty ekranu;
4. dokumentacja konkretnego wdrożenia;
5. jednoznaczne decyzje użytkownika.

Aktualny JSON jest nadrzędnym źródłem:

- treści strony;
- nazw usług;
- nazw modułów;
- hostów;
- kont użytkowników;
- ścieżek;
- komend;
- parametrów;
- wartości;
- wersji;
- numeracji;
- kolejności kroków.

Oficjalna dokumentacja produktu może służyć do poznawania standardowego działania technologii. Nie potwierdza konfiguracji konkretnego środowiska użytkownika.

Jeżeli dokumentacja produktu różni się od aktualnej instrukcji:

1. zachowaj wartość z aktualnej instrukcji;
2. pokaż rozbieżność użytkownikowi;
3. wskaż oficjalne źródło;
4. nie poprawiaj instrukcji bez decyzji użytkownika.

---

## Granice analizy

Agent może:

- wykrywać sprzeczności;
- porównywać fragmenty instrukcji;
- sprawdzać kolejność czynności;
- wskazywać brakujące informacje;
- porównywać tabelę z częścią opisową;
- sprawdzać zgodność komend z nazwami usług;
- wskazywać dane wymagające potwierdzenia;
- proponować decyzje.

Agent nie może samodzielnie:

- poprawiać nazw usług;
- zmieniać hostów;
- przenosić hostów pomiędzy środowiskami;
- zmieniać kont użytkowników;
- poprawiać komend;
- zmieniać ścieżek;
- dodawać brakujących parametrów;
- wymyślać brakujących danych;
- zastępować danych z JSON-u przykładami internetowymi;
- dodawać wyników analizy do Confluence.

---

## Etap 1 — identyfikacja zakresu instrukcji

Przed analizą ustal:

- tytuł instrukcji;
- system lub produkt;
- cel procedury;
- środowiska;
- moduły;
- usługi;
- role i konta;
- wymagania wstępne;
- oczekiwany rezultat;
- sposób weryfikacji rezultatu;
- dostępne materiały dodatkowe.

Jeżeli zakresu nie można ustalić, zgłoś niejasność. Nie uzupełniaj zakresu przypuszczeniami.

---

## Etap 2 — inwentaryzacja danych technicznych

Utwórz listę elementów występujących w instrukcji:

- rozdziały i podrozdziały;
- kroki proceduralne;
- moduły;
- usługi;
- procesy;
- hosty;
- środowiska;
- konta;
- komendy;
- argumenty;
- ścieżki;
- pliki;
- porty;
- adresy URL;
- nazwy pakietów;
- wersje;
- placeholdery;
- logi;
- alarmy;
- elementy monitoringu;
- oczekiwane wyniki;
- wartości kontrolne.

Lista jest podstawą analizy oraz późniejszej kontroli kompletności.

---

## Etap 3 — kontrola nazewnictwa

Sprawdź, czy ten sam element ma spójną nazwę w całej instrukcji.

Porównaj:

- tabelę z częścią opisową;
- nagłówki z komendami;
- nazwy modułów z nazwami usług;
- nazwy plików z używanymi ścieżkami;
- nazwy środowisk w różnych rozdziałach;
- nazwy pakietów w komendach i przykładach.

Zwróć szczególną uwagę na:

- myślniki i podkreślenia;
- końcówki `.service` i `.target`;
- literówki w nazwach;
- różnice wielkości liter;
- dodatkowe prefiksy;
- różne nazwy tego samego modułu;
- podobne nazwy mogące oznaczać inne obiekty.

Nie poprawiaj wykrytej różnicy. Umieść ją w raporcie.

---

## Etap 4 — kontrola hostów i środowisk

Sprawdź:

- czy każdy host jest przypisany do środowiska;
- czy ten sam host nie występuje w sprzecznych środowiskach;
- czy host z tabeli pojawia się w odpowiedniej procedurze;
- czy host opisany w tekście znajduje się w tabeli, jeżeli powinien;
- czy lista hostów jest spójna pomiędzy rozdziałami;
- czy wartości `PROD`, `Gold`, `Test` i `DEV` są stosowane konsekwentnie;
- czy opis „wszystkie serwery” nie jest sprzeczny z ograniczoną listą hostów.

Nie wyprowadzaj środowiska wyłącznie z nazwy hosta, jeśli materiał nie daje wystarczającego potwierdzenia.

---

## Etap 5 — kontrola kont i uprawnień

Dla każdego działania ustal:

- konto wykonujące czynność;
- wymaganie użycia `sudo`;
- ewentualne przełączenie użytkownika;
- środowisko;
- rodzaj usługi: systemowa czy użytkownika.

Sprawdź:

- czy konto w tabeli jest zgodne z opisem;
- czy przełączenie konta występuje przed komendą;
- czy `systemctl --user` jest używane w odpowiednim kontekście;
- czy polecenie systemowe nie zostało opisane jako polecenie użytkownika;
- czy konto dla produkcji i środowisk nieprodukcyjnych jest opisane spójnie;
- czy instrukcja nie wymaga uprawnienia, którego wcześniej nie wskazuje.

Nie przypisuj konta na podstawie podobnych procedur.

---

## Etap 6 — kontrola komend

Dla każdej komendy ustal:

- działanie;
- usługę lub proces;
- wymagane konto;
- środowisko;
- zależność od wcześniejszego kroku;
- oczekiwany rezultat.

Sprawdź:

- czy `start`, `stop`, `status` i `restart` dotyczą właściwej usługi;
- czy komendy dla tego samego modułu używają tej samej nazwy jednostki;
- czy komenda odpowiada opisanej czynności;
- czy ścieżki w komendzie są zgodne z tekstem;
- czy placeholder został wyjaśniony;
- czy przykład używa właściwej składni;
- czy polecenie nie zostało uszkodzone przez automatyczny link;
- czy podział wiersza nie występuje w środku ścieżki, URL lub nazwy usługi;
- czy operator przekierowania należy do tej samej komendy;
- czy kolejność komend jest zgodna z opisaną procedurą.

Nie wykonuj komend. Oceniaj wyłącznie spójność materiału.

---

## Etap 7 — kontrola kolejności czynności

Sprawdź, czy procedurę można wykonać w przedstawionej kolejności.

Weryfikuj między innymi:

1. czy wymagane logowanie następuje przed komendą;
2. czy przełączenie konta następuje przed użyciem tego konta;
3. czy zatrzymanie procesu występuje przed czynnością wymagającą zatrzymania;
4. czy uruchomienie występuje po zmianie konfiguracji lub czyszczeniu;
5. czy status jest sprawdzany we właściwym momencie;
6. czy weryfikacja następuje po uruchomieniu;
7. czy plik zostaje pobrany przed jego analizą;
8. czy porównywane wartości zostały wcześniej uzyskane;
9. czy późniejszy krok nie wymaga danych, których instrukcja wcześniej nie dostarcza;
10. czy operacja końcowa nie występuje przed czynnością przygotowawczą.

---

## Etap 8 — wymagania wstępne

Sprawdź, czy instrukcja podaje informacje konieczne do wykonania konkretnych kroków:

- wymagane konto;
- uprawnienia;
- dostęp do hosta;
- dostęp do repozytorium;
- dostęp do monitoringu;
- wymagane narzędzia;
- katalog roboczy;
- okno serwisowe;
- wymagane dane wejściowe.

Nie wymagaj uniwersalnego zestawu rozdziałów. Zgłaszaj tylko brak mający znaczenie dla wykonywanej procedury.

---

## Etap 9 — kontrola rezultatu

Sprawdź, czy instrukcja określa sposób potwierdzenia powodzenia operacji.

Weryfikacja może obejmować:

- status usługi;
- dostępność aplikacji;
- obecność procesu;
- logi;
- monitoring;
- alarmy;
- pliki błędów;
- wynik komendy;
- porównanie wartości;
- zgodność pakietów.

Brak weryfikacji po operacji o istotnym wpływie zgłoś jako brak lub sugestię zależnie od możliwych konsekwencji.

---

## Etap 10 — kontrola logów

Sprawdź:

- czy ścieżka logów jest zgodna pomiędzy tabelą i tekstem;
- czy ścieżka odpowiada właściwemu modułowi;
- czy względna ścieżka ma określony kontekst;
- czy wymagane jest przełączenie konta;
- czy plik logu w przekierowaniu odpowiada opisowi;
- czy instrukcja wskazuje, czego należy szukać w logach, jeśli jest to konieczne do weryfikacji.

Nie zamieniaj ścieżki na wartość z Internetu ani dokumentacji innego wdrożenia.

---

## Etap 11 — monitoring i alarmy

Sprawdź:

- czy wiadomo, jaki host monitorować;
- czy wskazano właściwy element;
- czy alarm ma jednoznaczną nazwę;
- czy wiadomo, jaki stan oznacza problem;
- czy kontrola następuje po odpowiednim kroku;
- czy plik, alarm albo wykres dotyczą właściwego modułu;
- czy użytkownik może odnaleźć wskazany widok.

Jeżeli potrzebne są dodatkowe dane, wskaż dokładnie:

- host;
- element;
- alarm;
- wykres;
- zakres czasu;
- potrzebny zrzut;
- potrzebny link do widoku.

Nie twierdź, że monitoring został sprawdzony bez otrzymania danych.

---

## Etap 12 — zgodność tabeli z tekstem

Porównaj:

- nazwy modułów;
- hosty;
- środowiska;
- konta;
- usługi;
- komendy;
- ścieżki logów;
- sposób restartu;
- wyjątki środowiskowe;
- sposób weryfikacji.

Różnice pomiędzy tabelą i częścią opisową traktuj jako możliwą sprzeczność wewnętrzną.

---

## Etap 13 — kontrola przykładów

Sprawdź, czy przykład:

- wykorzystuje nazwę zgodną z opisem;
- ma właściwy format;
- odpowiada przedstawionej składni;
- zawiera oczekiwany rodzaj wyniku;
- nie wprowadza innego pakietu lub usługi bez wyjaśnienia;
- nie jest przedstawiony jako wartość aktualna, jeżeli ma znaczenie wyłącznie przykładowe.

Nie zmieniaj przykładowych wartości bez polecenia użytkownika.

---

## Klasyfikacja problemów

### Błąd krytyczny

Problem mogący prowadzić do:

- operacji na niewłaściwym środowisku;
- użycia niewłaściwej usługi;
- wykonania błędnej komendy;
- utraty danych;
- istotnej niedostępności;
- pominięcia ważnego zabezpieczenia;
- publikacji na niewłaściwej stronie.

Nierozwiązany błąd krytyczny blokuje `PUBLISH`.

### Sprzeczność

Dwa fragmenty instrukcji podają różne informacje dotyczące tego samego elementu.

### Brak

Instrukcja nie zawiera informacji potrzebnej do jednoznacznego wykonania konkretnego kroku.

### Niejasność

Treść może być rozumiana na kilka sposobów albo nie pozwala potwierdzić właściwej interpretacji.

### Sugestia

Zmiana poprawiająca czytelność lub użyteczność, która nie wynika z potwierdzonego błędu.

Sugestii nie przedstawiaj jako obowiązkowych poprawek.

---

## Poziom wpływu

Każdemu problemowi przypisz wpływ:

- **Wysoki** — może doprowadzić do błędnej operacji, utraty danych albo istotnej niedostępności;
- **Średni** — może utrudnić wykonanie procedury lub spowodować niewłaściwą interpretację;
- **Niski** — dotyczy głównie precyzji, czytelności albo wygody.

---

## Poziom pewności

Każdy problem oznacz jako:

- **Potwierdzony** — wynika bezpośrednio z dostępnych materiałów;
- **Prawdopodobny** — wynika z logicznego porównania informacji;
- **Do weryfikacji** — brakuje danych do potwierdzenia.

Nie przedstawiaj podejrzenia jako potwierdzonego błędu.

---

## Format raportu

Raport powinien zawierać:

1. Błędy krytyczne;
2. Sprzeczności;
3. Braki;
4. Niejasności;
5. Sugestie;
6. Brakujące materiały;
7. Kontrole niewykonane.

Każdy problem przedstaw według wzoru:

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
