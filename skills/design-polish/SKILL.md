---
name: design-polish
description: Automatyzuje stylistyczny "design pass" po pierwszej iteracji UI w projekcie — dostylowuje istniejący produkt do spójnego standardu opisanego w DESIGN.MD, bez ruszania layoutu. Użyj tego skilla gdy: (1) użytkownik kończy pierwszą iterację/prototyp UI i mówi "dostyluj UI", "wypoleruj wygląd", "zrób design pass", "ujednolić styl", "zastosuj design system"; (2) użytkownik wspomina o kończeniu/domykaniu iteracji projektu w kontekście frontendu/UI, nawet bez wprost proszenia o styl, jeśli w projekcie jest świeżo zbudowany interfejs; (3) w projekcie istnieje lub powinien powstać plik DESIGN.MD jako source of truth dla wyglądu. Skill sprawdza, czy DESIGN.MD już istnieje, audytuje UI względem niego (pokryte / brakujące / konfliktowe), ZAWSZE dopytuje użytkownika zanim wprowadzi cokolwiek niejednoznacznego, wprowadza styl bez zmiany struktury/layoutu, i na końcu aktualizuje DESIGN.MD tak by pozostał kompletnym i aktualnym standardem.
---

# design-polish

## Kiedy się uruchamia

- Wprost: "dostyluj UI", "design pass", "wypoleruj wygląd", "ujednolić styl w projekcie", "zastosuj design system".
- Pośrednio: użytkownik mówi, że kończy/domyka pierwszą iterację, prototyp albo wersję roboczą projektu, a w projekcie jest UI (komponenty, strony, panele) — nawet jeśli nie użył słowa "styl". W takim wypadku krótko zaproponuj design pass zamiast zakładać, że o to nie chodzi.

## Krok 0 — sprawdź, czy `DESIGN.MD` istnieje w projekcie

Poszukaj pliku `DESIGN.MD` w katalogu głównym projektu (i pomocniczo w typowych miejscach: `/docs`, `/design`, `.claude/`).

**Jeśli `DESIGN.MD` istnieje** → przejdź do Kroku 1, traktując go jako standard/source of truth.

**Jeśli `DESIGN.MD` NIE istnieje** → zawsze zatrzymaj się i zapytaj użytkownika, zanim cokolwiek wygenerujesz albo zmienisz w UI:

> "W projekcie nie ma jeszcze `DESIGN.MD`. Chcesz:
> (a) bazowy `DESIGN.MD` z szablonu tego skilla (monochromatyczny, dark-only system — patrz `templates/DESIGN.baseline.md`), czy
> (b) żebym wygenerował `DESIGN.MD` na bazie tego, co już jest w Twoim UI (wyciągnę realne kolory, fonty, promienie, cienie z obecnego kodu i złożę je w tokeny)?"

Nie zgaduj sam, którą opcję wybrać, i nie mieszaj obu bez potwierdzenia. Po odpowiedzi:
- (a) → skopiuj `templates/DESIGN.baseline.md` do katalogu głównego projektu jako `DESIGN.MD`.
- (b) → przeanalizuj istniejące style (CSS/Tailwind config/styled-components/tokeny w kodzie), wyodrębnij realnie używane wartości kolorów, typografii, promieni, cieni, odstępów, zbuduj z nich `DESIGN.MD` w tej samej strukturze co szablon (frontmatter z tokenami + sekcje Kolory/Typografia/Kształty/Komponenty), i pokaż użytkownikowi do akceptacji PRZED użyciem go do stylowania.

Dopiero mając zaakceptowany `DESIGN.MD` przechodzisz dalej.

## Krok 1 — audyt UI względem `DESIGN.MD` (obowiązkowy, przed jakąkolwiek zmianą)

Przejrzyj całe UI projektu i porównaj z `DESIGN.MD`. Podziel wynik na trzy kategorie i przedstaw użytkownikowi:

1. **Pokryte wprost** — komponenty z jasnym odpowiednikiem w `DESIGN.MD` (button, select, toggle, slider itd.). Krótka lista.
2. **Brakujące w spec** — elementy UI, których `DESIGN.MD` nie opisuje (modal, tooltip, tabela, notyfikacje, badge, karta, wykres, empty state, loader, breadcrumb itd.). Dla każdego: jak wygląda dziś + Twoja propozycja stylu wyprowadzona z ogólnych zasad pliku (paleta, rampa alfy, typografia, promienie, jedna głębia) — bez wdrażania.
3. **Niejednoznaczne / konfliktowe** — miejsca kolidujące z zasadami (lokalne cienie, dodatkowy kolor akcentu, inny sposób oznaczania aktywności, czwarty rozmiar fontu) — bez jednoznacznego rozstrzygnięcia.

## Krok 2 — dopytaj, zanim ruszysz kod

Dla punktów 2 i 3 z Kroku 1: **zatrzymaj się i zadaj konkretne pytania**, po kolei, z propozycją rozwiązania do wyboru (np. "modal: `.surface` + jeden ambient shadow, czy inny wariant głębi?"). Nie zaczynaj implementacji, dopóki użytkownik nie odpowie.

## Krok 3 — implementacja (dopiero po Krokach 0–2)

Zasady twarde, obowiązują zawsze:

1. **Nie zmieniaj layoutu.** Struktura DOM, rozmieszczenie sidebarów/paneli, kolejność sekcji, `position`, `top/right/left/bottom`, szerokości/wysokości kontenerów układu, breakpointy układu strony — zostają nietknięte. Zmieniasz wyłącznie warstwę wizualną (kolor, typografia, obramowanie, cień, radius, przejścia, stany).
2. **Tylko tokeny z `DESIGN.MD`.** Żadnych nowych kolorów, rozmiarów fontu, promieni, cieni spoza pliku. Brakujący przypadek → najbliższy istniejący token, nie nowa wartość.
3. **Monochrom / dark-only** (o ile `DESIGN.MD` tak stanowi) — usuń kolory marki/akcenty/gradienty spoza pliku.
4. **Aktywność = inwersja** (biały fill + czarna treść), zgodnie z sekcją "Aktywne = inwersja" w pliku — nie wprowadzaj innego sygnału stanu.
5. **Tylko tyle rozmiarów typografii, ile ma `DESIGN.MD`** — zmapuj istniejące teksty na te poziomy.
6. **Jedna głębia w całej aplikacji** (`ambient` shadow na powierzchni) — usuń pozostałe `box-shadow` per-element.
7. **`DESIGN.MD` musi zostać zaktualizowany.** Każda nowa reguła/wyjątek ustalony w Kroku 2 wraca do pliku (nowy wpis w `components:` + odpowiadająca sekcja CSS), zanim uznasz zadanie za skończone.

Przejdź komponent po komponencie: znajdź odpowiednik w `DESIGN.MD` → zastosuj dokładnie tę specyfikację (kolor, obramowanie, radius, wysokość, transitions, stany hover/focus/active/disabled). Zaimportuj font i zmienne `:root` z sekcji "Fundamenty", jeśli projekt ich jeszcze nie ma; jeśli ma podobne pod innymi nazwami — ujednolić wartości zamiast masowo zmieniać nazwy zmiennych w kodzie (ryzyko regresji).

## Zabronione

- Zmiana układu stron/widoków, nawigacji, hierarchii komponentów w drzewie DOM.
- Nowe kolory/rozmiary fontu/cienie spoza `DESIGN.MD`.
- Zmiana logiki/zachowania komponentów — tylko styl.
- Wdrażanie punktów z kategorii 2/3 (Krok 1) bez odpowiedzi użytkownika z Kroku 2.

## Na koniec

Krótkie podsumowanie: które pliki/komponenty zmieniono, jakie były przypadki bez jednoznacznego odpowiednika i jak je rozstrzygnięto, oraz potwierdzenie, że wszystkie te ustalenia trafiły z powrotem do `DESIGN.MD`.

## Pliki pomocnicze tego skilla

- `templates/DESIGN.baseline.md` — bazowy, monochromatyczny `DESIGN.MD` używany w opcji (a) z Kroku 0.
