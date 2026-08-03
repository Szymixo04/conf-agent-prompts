# Standard wizualny instrukcji Confluence

> **Status:** OSTATECZNY / AKTUALNY  
> **Wersja:** 2.0  
> **Przeznaczenie:** Publiczny standard pracy agenta modernizującego instrukcje Confluence  
> **Bezpieczeństwo:** Dokument nie zawiera danych organizacyjnych ani danych dostępowych  
> **Zasada nadrzędna:** Materiały bieżącego zadania mają pierwszeństwo przed neutralnymi przykładami.

## Cel

Standard poprawia czytelność bez zmiany znaczenia technicznego. Ochrona treści ma pierwszeństwo przed wyglądem.

## Zasada minimalnej zmiany

Najpierw popraw element powodujący problem. Nie przebudowuj całej tabeli z powodu jednej długiej komendy. Nie łącz kolumn, nie usuwaj wierszy i nie przenoś sekcji bez decyzji użytkownika.

## Struktura

Zachowaj główne rozdziały, ich kolejność i numerację. Stosuj spójną hierarchię:

- H1 — główne rozdziały;
- H2 — bezpośrednie podrozdziały;
- H3 — sekcje wewnętrzne.

Nie dodawaj brakujących rozdziałów tylko dlatego, że występują w innym wzorcu.

## Akapity i listy

Jeden akapit powinien opisywać jedną powiązaną kwestię. Nie oddzielaj warunku od czynności ani ostrzeżenia od operacji.

Używaj list punktowanych, gdy kolejność nie jest istotna, i numerowanych, gdy kroki zależą od siebie. Nie zamieniaj sekwencji komend na listę numerowaną.

## Tabele

Zachowaj:

- liczbę i znaczenie kolumn;
- kolejność kolumn;
- wszystkie wiersze i komórki;
- hosty, konta, komendy i logi.

Nie usuwaj kolumny „Położenie logów”. Nie łącz jej z nazwą modułu tylko po to, aby zwęzić tabelę.

Tabela powinna mieścić się w obszarze treści. W razie problemu:

1. znajdź element rozszerzający tabelę;
2. popraw prezentację długiej komendy;
3. zastosuj kontrolowane podziały linii;
4. skoryguj proporcje kolumn;
5. zachowaj układ merytoryczny.

Kolumna komend zwykle wymaga największej szerokości, ale proporcje mają wynikać z rzeczywistej zawartości.

## Grupowanie środowisk

Stosuj:

```text
PROD:
host-prod-01.example.local
host-prod-02.example.local

Gold:
host-gold-01.example.local

Test:
host-test-01.example.local

DEV:
host-dev-01.example.local
```

Nazwę środowiska pokazuj raz dla grupy. Zachowaj hosty i ich przypisanie. Nie twórz środowisk ani hostów. Wiersz „Wszystkie serwery” pozostaw bez sztucznego podziału.

## Konta

Zachowuj dokładne wartości kont i ich zależność od środowiska. Nie interpretuj nazw kont jako imion lub ról.

## Kod liniowy

Stosuj dla krótkich elementów w zdaniu lub komórce:

- nazw usług;
- ścieżek;
- plików;
- rozszerzeń;
- krótkich parametrów.

## Natywne makro Code

Poza szerokimi tabelami stosuj makro Code dla gotowych poleceń, sekwencji i przykładowych wyników. Dla powłoki używaj języka `bash`, jeśli pasuje do źródła.

Tytuł dodawaj tylko na polecenie użytkownika albo zgodnie z zaakceptowanym wzorcem. Nie tytułuj automatycznie wszystkich bloków.

## Kod w tabeli

Jeżeli natywne makro Code rozszerza tabelę, użyj prostszego kodu z zachowanymi liniami. Kod musi pozostać kopiowalny i nie może tracić znaków.

## Długie polecenia

Nie dziel:

- hosta;
- ścieżki;
- nazwy pliku lub pakietu;
- nazwy usługi;
- URL;
- operatora przekierowania.

Jeżeli polecenie ma być kopiowane jako wieloliniowe, zachowaj poprawną składnię powłoki, na przykład przez backslash. Nie dodawaj nowych argumentów.

## Makra

### Note

Do ważnej informacji wymagającej uwagi przed procedurą, na przykład wpływu restartu lub wymaganego okna serwisowego.

### Info

Do informacji pomocniczej, która nie jest ostrzeżeniem.

### Warning

Tylko gdy źródło wyraźnie opisuje ryzyko albo użytkownik zlecił wyróżnienie.

### Tip

Do opcjonalnej wskazówki. Nie używaj dla czynności obowiązkowej.

Makra nie mogą zawierać uwag redakcyjnych, raportu analizy ani opisu modernizacji.

## Kontrola kompletności tabeli

Przed zmianą zapisz:

- liczbę kolumn i wierszy;
- nagłówki;
- moduły;
- hosty;
- konta;
- komendy;
- ścieżki logów.

Po zmianie porównaj te elementy semantycznie.

## Kontrola widoku

Po zapisaniu strony testowej sprawdź widoczność wszystkich kolumn, pełnych hostów, komend i logów oraz brak poziomego rozszerzenia przez kod. Jeżeli nie wykonano podglądu, zaznacz to w raporcie.

---

## Powiązane moduły

- [Strona główna standardu](index.html)
- [Analiza merytoryczna](analiza-merytoryczna.html)
- [Standard wizualny](standard-wizualny.html)
- [Format Confluence](format-confluence.html)
- [Code review](code-review.html)
- [Znane błędy](znane-bledy.html)

## Wzorzec decyzji wizualnej

Przed zmianą elementu ustal jego funkcję:

- treść proceduralna;
- wartość techniczna;
- ostrzeżenie;
- przykład;
- wynik polecenia;
- lista obiektów;
- odwołanie do dokumentu.

Dobierz format do funkcji. Nie formatuj wszystkich elementów technicznych w identyczny sposób.

## Nagłówki i numeracja

Nagłówki mają odzwierciedlać strukturę, a nie dekorację. Nie pomijaj poziomu bez potrzeby. Nie zamieniaj etykiety tabeli ani nazwy środowiska na nagłówek strony. Zachowaj numerację źródłową, chyba że użytkownik wyraźnie zatwierdzi reorganizację.

## Czytelność procedury

Oddziel opis od czynności wykonywalnej. Komendę umieść bezpośrednio po zdaniu wyjaśniającym cel, jeżeli źródło łączy te elementy. Ostrzeżenie umieść przed czynnością, której dotyczy. Wynik kontrolny umieść po komendzie.

## Tabele — test wymiarowy

Przed TEST sprawdź logicznie:

- czy żadna komórka nie zawiera niepodzielnego ciągu bez uzasadnienia;
- czy pełne hosty pozostają czytelne;
- czy kod nie wymusza minimalnej szerokości;
- czy nagłówki nie są znacznie dłuższe niż zawartość;
- czy kolumna logów pozostała dostępna.

Po TEST wykonaj rzeczywisty podgląd przy standardowym powiększeniu. Kontrola kodu nie zastępuje kontroli renderowania.

## Bloki Code — decyzja

Użyj bloku Code poza tabelą, gdy użytkownik ma skopiować polecenie lub wynik wymaga zachowania wierszy. Użyj kodu liniowego dla krótkiej nazwy. W tabeli użyj rozwiązania zawijanego tylko wtedy, gdy makro Code pogarsza szerokość.

Nie zmieniaj kilku oddzielnych komend w jedną komendę połączoną średnikiem, `&&` lub potokiem.

## Makra — test adekwatności

Przed dodaniem makra odpowiedz:

1. Czy informacja już istnieje w źródle?
2. Czy makro zmienia tylko widoczność, a nie znaczenie?
3. Czy typ makra odpowiada wadze informacji?
4. Czy treść nadal jest czytelna bez interpretacji agenta?

Jeżeli odpowiedź na którekolwiek pytanie jest negatywna, nie dodawaj makra bez decyzji użytkownika.

## Elementy niedozwolone

Nie dodawaj ozdobnych ikon, emoji, kolorów, ramek, nowych bannerów, podsumowań ani sekcji „Najważniejsze”, jeżeli nie wynikają ze standardu lub polecenia. Nie ukrywaj treści w rozwijanych sekcjach bez zatwierdzenia.

## Raport kontroli wizualnej

Podaj osobno:

- kontrole możliwe na podstawie Storage Format;
- kontrole wykonane na wyrenderowanej stronie;
- elementy wymagające oceny użytkownika;
- znane różnice pomiędzy widokiem testowym a źródłem.
