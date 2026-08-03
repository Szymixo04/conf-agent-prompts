# Confluence Storage Format

> **Status:** OSTATECZNY / AKTUALNY  
> **Wersja:** 2.0  
> **Przeznaczenie:** Publiczny standard pracy agenta modernizującego instrukcje Confluence  
> **Bezpieczeństwo:** Dokument nie zawiera danych organizacyjnych ani danych dostępowych  
> **Zasada nadrzędna:** Materiały bieżącego zadania mają pierwszeństwo przed neutralnymi przykładami.

## Cel

Moduł określa bezpieczne generowanie i kontrolę `body.storage.value` w formacie XHTML/XML używanym przez Confluence.

## Podstawowe zasady

Treść musi być poprawnym fragmentem XML po opakowaniu elementem nadrzędnym z przestrzeniami nazw `ac` i `ri`.

Sprawdzaj domknięcie:

- tabel, `tbody`, `tr`, `th` i `td`;
- nagłówków i akapitów;
- list;
- makr;
- `ac:parameter`;
- `ac:rich-text-body`;
- `ac:plain-text-body`;
- CDATA.

## Encje XML

W zwykłym XHTML koduj co najmniej:

```text
&  -> &amp;
<  -> &lt;
>  -> &gt;
"  -> &quot; w atrybutach
'  -> &apos; w atrybutach, gdy potrzebne
```

Nie koduj ponownie już poprawnie zakodowanych encji.

## CDATA

Treść bloku Code można umieszczać w `ac:plain-text-body` jako CDATA. Sprawdź, czy kod nie zawiera sekwencji:

```text
]]>
```

Jeżeli zawiera, nie twórz niepoprawnej sekcji. Podziel sekwencję bez zmiany tekstu albo zastosuj bezpieczne kodowanie.

## Makro Code

Neutralny wzorzec:

```xml
<ac:structured-macro ac:name="code">
  <ac:parameter ac:name="language">bash</ac:parameter>
  <ac:plain-text-body><![CDATA[example-command --flag value]]></ac:plain-text-body>
</ac:structured-macro>
```

Opcjonalny tytuł:

```xml
<ac:parameter ac:name="title">Przykładowy tytuł</ac:parameter>
```

Nie dodawaj tytułu bez potrzeby.

## Makro informacyjne

Neutralny wzorzec `note`:

```xml
<ac:structured-macro ac:name="note">
  <ac:parameter ac:name="title">Ważne</ac:parameter>
  <ac:rich-text-body>
    <p>Treść istniejącej ważnej informacji.</p>
  </ac:rich-text-body>
</ac:structured-macro>
```

Makro musi zawierać treść przeznaczoną dla czytelnika, nie komentarz o pracy agenta.

## Tabele

Każdy wiersz musi mieć właściwą liczbę komórek, chyba że źródło świadomie używa `rowspan` lub `colspan`.

Nie polegaj na nieobsługiwanych stylach CSS. Confluence może usunąć część stylów podczas zapisu.

Nie używaj stylu jako trwałej informacji kontrolnej.

## Kod w tabelach

Gdy makro Code powoduje nadmierną szerokość, dopuszczalna jest prostsza struktura:

```xml
<div><code>line-1<br/>line-2</code></div>
```

Przed wstawieniem ucieknij znaki XML. Zachowaj linie, kolejność i treść komendy.

## Automatyczne linki

Komenda zawierająca URL nie może zostać przekształcona w element `a` ani wzbogacona klasami interfejsu. Przed publikacją wyszukaj w kodzie wejściowym i wyniku podejrzane fragmenty:

```text
<a href=
class="fai-
target="_blank"
rel="noopener noreferrer"
```

Ich obecność w przejętym tekście komendy oznacza uszkodzenie materiału.

## Walidacja przed zapisem

1. Znormalizuj wyłącznie nieobsługiwane nazwane encje HTML do wartości XML.
2. Opakuj fragment elementem `root` z przestrzeniami nazw.
3. Parsuj jako `application/xml`.
4. Przerwij przy `parsererror`.
5. Sprawdź ręcznie poprawność makr i CDATA.

Walidacja XML nie zastępuje kontroli znaczenia.

## Normalizacja po zapisie

Confluence może zmienić:

```text
<br/>       -> <br />
ó           -> &oacute;
<           -> &lt;
>           -> &gt;
&           -> &amp;
```

Może również zmienić odstępy, kolejność atrybutów i usunąć style.

Nie porównuj całego HTML znak po znaku.

## Walidacja semantyczna

Po zapisie:

1. pobierz ponownie `body.storage.value`;
2. dekoduj encje HTML;
3. normalizuj spacje i białe znaki;
4. sprawdź trwałe wartości;
5. oddziel brak treści od różnicy technicznego zapisu.

Nie waliduj obecności dokładnych fragmentów zawierających `<br>`, `<strong>`, style lub kolejność atrybutów.

## Kontrola wyniku

Sprawdź:

- możliwość ponownego parsowania XML;
- obecność nagłówków;
- liczbę wierszy i kolumn;
- obecność makr;
- treść bloków kodu;
- brak automatycznych linków;
- hosty, usługi, komendy, ścieżki i wartości.

---

## Powiązane moduły

- [Strona główna standardu](index.html)
- [Analiza merytoryczna](analiza-merytoryczna.html)
- [Standard wizualny](standard-wizualny.html)
- [Format Confluence](format-confluence.html)
- [Code review](code-review.html)
- [Znane błędy](znane-bledy.html)

## Przestrzenie nazw do walidacji lokalnej

Do parsowania fragmentu użyj neutralnego elementu nadrzędnego:

```xml
<root xmlns:ac="http://atlassian.com/content" xmlns:ri="http://atlassian.com/resource/identifier">
  <!-- body.storage.value -->
</root>
```

Element nadrzędny służy walidacji i nie jest wysyłany jako treść strony.

## Funkcje kodujące

Rozdziel funkcje:

- kodowanie tekstu XML;
- kodowanie wartości atrybutu;
- przygotowanie CDATA;
- normalizacja tekstu do porównania;
- dekodowanie encji po GET.

Nie używaj jednej funkcji do wszystkich kontekstów. Szczególnie nie koduj zawartości CDATA jak zwykłego XHTML i nie wkładaj niesprawdzonego tekstu do atrybutu.

## Named entities

Parser XML nie rozpoznaje wszystkich nazwanych encji HTML bez definicji DTD. Przed lokalnym parsowaniem można zamienić wyłącznie znane, poprawne encje HTML na znaki Unicode lub encje numeryczne. Nie wykonuj globalnej zamiany każdego `&`, ponieważ może to spowodować podwójne kodowanie.

## Kontrola tabel

Dla każdej tabeli policz logicznie liczbę komórek w wierszach. Uwzględnij świadome `colspan` i `rowspan`. Sprawdź obecność `tbody`, jeżeli jest wymagany przez przyjęty wzorzec, oraz brak komórek umieszczonych poza wierszem.

## Kontrola makr

Dla każdego makra sprawdź:

- `ac:name`;
- unikalność parametrów, jeżeli parametr nie może się powtarzać;
- zgodność rodzaju body z makrem;
- brak `ac:rich-text-body` wewnątrz `ac:plain-text-body`;
- poprawne granice CDATA;
- zachowanie treści po ponownym GET.

## Bezpieczne porównanie komend

Do walidacji semantycznej komendy:

1. dekoduj encje;
2. zamień kontrolowane `<br>` na znak nowej linii;
3. usuń wyłącznie prezentacyjne znaczniki;
4. normalizuj końce linii;
5. porównaj tokeny i znaki znaczące;
6. nie usuwaj cudzysłowów, backslashy ani operatorów.

## Payload

Wartość `body.storage.representation` ma być zgodna z interfejsem używanym przez instalację Confluence. Nie dodawaj pól niewymaganych przez źródłowy obiekt. Tytuł i ancestors pobierz ze świeżej strony, nie z historycznego przykładu.

## Testy negatywne

Walidator powinien odrzucić co najmniej:

- niedomkniętą tabelę;
- niezamknięte CDATA;
- nagi znak `&`;
- komórkę poza `tr`;
- automatyczny link wewnątrz komendy;
- brak wymaganego parametru makra;
- utratę chronionego hosta lub polecenia.

## Raport walidacji

Wynik rozdziel na:

- poprawność XML;
- poprawność struktur Confluence;
- kompletność danych;
- udany zapis;
- poprawność odczytu po zapisie;
- kontrolę renderowania.

Pozytywny wynik jednej warstwy nie oznacza automatycznie pozytywnego wyniku pozostałych.
