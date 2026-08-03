# Znane błędy i rozwiązania

## Cel

Moduł opisuje powtarzalne problemy podczas generowania, zapisywania i walidowania treści Confluence. Najpierw ustal faktyczny etap błędu. Nie wykonuj automatycznie kolejnego PUT.

## 1. `<br/>` kontra `<br />`

### Objaw

Walidator zgłasza brak fragmentu zawierającego `<br/>`, mimo że treść jest widoczna.

### Przyczyna

Confluence znormalizował znacznik do `<br />`.

### Rozwiązanie

Nie sprawdzaj dokładnego fragmentu HTML. Dekoduj treść, normalizuj białe znaki i waliduj trwałe dane po obu stronach znacznika.

## 2. Polskie znaki jako encje

### Objaw

Walidator nie znajduje tekstu, na przykład „Położenie logów”.

### Przyczyna

Confluence zwrócił `Położenie log&oacute;w`.

### Rozwiązanie

Przed porównaniem dekoduj encje HTML i normalizuj spacje.

## 3. Placeholder zakodowany jako XML

### Objaw

Walidator nie znajduje `kill -9 <process_id>`.

### Przyczyna

W Storage Format zapisano `&lt;process_id&gt;`.

### Rozwiązanie

Porównuj znormalizowaną treść po dekodowaniu encji. Nie porównuj surowego kodowania.

## 4. Walidacja nieobsługiwanego CSS

### Objaw

Po zapisie brakuje `overflow-wrap: anywhere` albo innej właściwości.

### Przyczyna

Confluence usunął nieobsługiwany styl.

### Rozwiązanie

Nie używaj CSS jako wymaganego elementu walidacji. Sprawdzaj treść i strukturę, a wygląd oceń w rzeczywistym podglądzie.

## 5. Automatyczny link w komendzie

### Objaw

W komendzie pojawiają się elementy `a`, `target`, `rel`, `title` lub klasy interfejsu.

### Przyczyna

Adres URL został automatycznie wzbogacony przez edytor lub czat przed użyciem jako kod.

### Rozwiązanie

Odtwórz komendę z czystego tekstu źródłowego. W bloku Code umieść URL w CDATA. Przed publikacją wyszukaj podejrzane elementy HTML i klasy interfejsu.

## 6. Natywne makro Code rozszerza tabelę

### Objaw

Kolumna z logami jest poza ekranem, a tabelę widać dopiero po silnym zmniejszeniu powiększenia.

### Przyczyna

Makro Code albo długa niepodzielna komenda narzuca minimalną szerokość komórki.

### Rozwiązanie

Nie zmieniaj układu tabeli. W tabeli zastosuj prostszy kod z kontrolowanymi podziałami linii. Poza tabelą zachowaj natywne makro Code.

## 7. Niebezpieczny podział komendy

### Objaw

Ścieżka, URL lub nazwa usługi zostały rozdzielone w środku.

### Przyczyna

Podział wykonano według szerokości tekstu, a nie składni polecenia.

### Rozwiązanie

Dziel tylko pomiędzy argumentami. Jeśli wynik ma być kopiowany jako jedna komenda, zastosuj poprawną kontynuację powłoki. Porównaj oryginał z wersją po usunięciu kontrolowanych podziałów.

## 8. PUT się udał, ale walidacja zgłosiła błąd

### Objaw

Skrypt zgłasza błąd „Po zapisie brakuje informacji”, lecz numer wersji wzrósł.

### Przyczyna

Zapis został wykonany, a błąd dotyczy zbyt kruchej walidacji.

### Rozwiązanie

Nie ponawiaj PUT. Pobierz stronę ponownie, sprawdź wersję i treść semantycznie, a następnie popraw walidator.

## 9. Dokładny fragment HTML w `requiredTexts`

### Objaw

Walidator szuka tekstu zawierającego `strong`, `br` lub style.

### Przyczyna

Lista kontrolna opisuje sposób renderowania zamiast trwałej informacji.

### Rozwiązanie

W `requiredTexts` przechowuj hosty, nazwy usług, ścieżki, wartości i istotne zdania. Strukturę HTML sprawdzaj osobno parserem.

## 10. Usunięte bloki Code poza tabelą

### Objaw

Komendy w rozdziałach opisowych są zwykłym tekstem.

### Przyczyna

Funkcja przeznaczona dla kodu w tabeli została zastosowana globalnie.

### Rozwiązanie

Używaj dwóch funkcji: natywnego makra Code poza tabelą oraz zawijanego kodu wewnątrz tabeli. Testuj liczbę i lokalizację makr.

## 11. Tytuły dodane do wszystkich bloków

### Objaw

Każdy blok Code ma zbędny tytuł.

### Przyczyna

Jedna funkcja generująca tytuł została użyta globalnie.

### Rozwiązanie

Oddziel blok zwykły od bloku tytułowanego. Tytuły stosuj tylko według polecenia lub zaakceptowanego wzorca.

## 12. Powtarzane etykiety środowisk

### Objaw

Każdy host ma osobne `PROD:`.

### Przyczyna

Etykieta została przypisana do hosta zamiast grupy.

### Rozwiązanie

Grupuj kolejno hosty tego samego środowiska. Porównaj pełną listę hostów przed i po transformacji.

## 13. Uszkodzony JSON lub treść z czatu

### Objaw

W danych pojawiają się znaczniki HTML, linki, klasy interfejsu albo ucięte ciągi.

### Przyczyna

Materiał skopiowano z widoku renderowanego zamiast czystej odpowiedzi API.

### Rozwiązanie

Przerwij modernizację. Pobierz czysty JSON ponownie. Nie naprawiaj dużego uszkodzonego fragmentu przez zgadywanie.

## 14. Konflikt wersji strony

### Objaw

PUT zwraca błąd wersji albo grozi nadpisaniem nowszej zmiany.

### Przyczyna

Strona została zmieniona po przygotowaniu payloadu.

### Rozwiązanie

Pobierz świeżą stronę, porównaj zmiany i przygotuj nowy payload. Nie zwiększaj numeru wersji bez ponownego odczytu.

## 15. Błędny pageId

### Objaw

Skrypt pobiera lub aktualizuje inną stronę.

### Przyczyna

Zmieniono identyfikator bez kontroli ról strony źródłowej, testowej i docelowej.

### Rozwiązanie

Rozdziel identyfikatory, sprawdź `currentPage.id` i w trybie TEST zezwól na PUT tylko do skonfigurowanej strony testowej.

## Raport błędu

Podaj:

```text
Etap:
Czy PUT został wysłany:
Kod HTTP:
Wersja przed:
Wersja po:
Faktyczny stan strony:
Przyczyna:
Poprawka:
Test regresyjny:
```
