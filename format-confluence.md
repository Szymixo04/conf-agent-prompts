# Confluence Storage Format

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
