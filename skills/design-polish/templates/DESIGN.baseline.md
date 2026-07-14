---
version: alpha
name: Mono UI Style Kit
description: Uniwersalny, monochromatyczny system stylowania komponentów (dark-only). Nie zawiera layoutu ani pozycjonowania — dotyczy wyłącznie WYGLĄDU elementów (kolor, typografia, kształt, obramowania, stany). Nakładany na istniejący układ paneli/sidebarów bez zmiany ich rozmieszczenia.

# ⚠ STATUS: STANDARD / SOURCE OF TRUTH
# Ten plik jest jedynym źródłem prawdy dla wyglądu i spójności UI w projekcie.
# Każda decyzja stylistyczna (kolor, typografia, kształt, cień, stan interakcji)
# musi dać się wyprowadzić z tego pliku. Jeśli czegoś tu nie ma — patrz sekcja
# "Rozszerzanie standardu" na końcu dokumentu, zanim wprowadzisz coś nowego.

colors:
  primary: "#FFFFFF"      # Ink White — cały tekst, aktywne wypełnienia, obramowania suwaka/gałki, wypełnienie przycisku
  neutral: "#000000"      # Canvas Black — tło, wypełnienie opcji select, wypełnienie kciuka slidera i gałki toggle
  on-primary: "#000000"   # treść na białym tle (etykieta przycisku, aktywna etykieta segmentu) — kontrast 21:1

colors_alpha:
  secondary:     "rgba(255,255,255,0.70)"  # tekst drugorzędny, etykiety, linki reset, kciuk scrollbara
  border:        "rgba(255,255,255,0.30)"  # domyślne obramowanie kontrolek, tor slidera, placeholder
  border-panel:  "rgba(255,255,255,0.16)"  # obramowanie powierzchni "szklanej"
  divider:       "rgba(255,255,255,0.10)"  # linie sekcji / separatory
  hover-plate:   "rgba(255,255,255,0.08)"  # hover nieaktywnego przycisku w segmented control
  track-faint:   "rgba(255,255,255,0.05)"  # tor scrollbara
  credit-faint:  "rgba(255,255,255,0.35)"  # tekst pomocniczy / disabled note
  input-bg:      "rgba(0,0,0,0.50)"        # tło "wpuszczonych" kontrolek (select, toggle, input, color-control)
  surface-bg:    "rgba(1,1,1,0.12)"        # tło powierzchni "szklanej" (pod blur)

shadows:
  ambient: "rgba(0,0,0,0.40)"   # jedyny cień w systemie — box-shadow: 0 8px 32px {shadows.ambient}

effects:
  surface-blur: "blur(5px)"     # backdrop-filter na powierzchniach "szklanych"

typography:
  title:          # nagłówek / tytuł panelu
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 500
    lineHeight: 1.2
  section-label:  # etykiety sekcji
    fontFamily: Inter
    fontSize: 11px
    fontWeight: 400
    letterSpacing: 0.5px
    textTransform: uppercase
  body:           # etykiety kontrolek, wartości, tekst select/hex, etykiety przycisków
    fontFamily: Inter
    fontSize: 12px
    fontWeight: 400
  meta:           # linki, stopki, drobny tekst pomocniczy
    fontFamily: Inter
    fontSize: 11px
    fontWeight: 400
    letterSpacing: 0.5px
  button:         # przyciski akcji głównej
    fontFamily: Inter
    fontSize: 12px
    fontWeight: 700   # ⚠ patrz uwaga w sekcji Typografia

rounded:
  xs: 2px       # najmniejsze elementy (np. wnętrze swatcha koloru)
  sm: 3px       # przyciski, pigułka segmentu
  md: 6px       # standardowy promień kontrolek i powierzchni
  full: 9999px  # elementy binarne/przeciągane (toggle, kciuk slidera)

sizing:
  control-h: 32px     # kanoniczna wysokość kontrolki (input, select, button, toggle-track opcjonalnie mniejszy)
  unit: 4px           # bazowa jednostka odstępów wewnątrz komponentu (4 / 8 / 16)

components:
  surface:        { backgroundColor: "{colors_alpha.surface-bg}", border: "1px solid {colors_alpha.border-panel}", rounded: "{rounded.md}", textColor: "{colors.primary}" }
  button-primary: { backgroundColor: "{colors.primary}", textColor: "{colors.on-primary}", typography: "{typography.button}", rounded: "{rounded.sm}", height: "{sizing.control-h}" }
  select:         { backgroundColor: "{colors_alpha.input-bg}", border: "1px solid {colors_alpha.border}", rounded: "{rounded.md}", typography: "{typography.body}", height: "{sizing.control-h}" }
  segmented:      { backgroundColor: "{colors_alpha.input-bg}", border: "1px solid {colors_alpha.border}", rounded: "{rounded.md}", height: "{sizing.control-h}" }
  toggle:         { backgroundColor: "{colors_alpha.input-bg}", border: "1px solid {colors_alpha.border}", rounded: "{rounded.full}" }
  color-control:  { backgroundColor: "{colors_alpha.input-bg}", border: "1px solid {colors_alpha.border}", rounded: "{rounded.md}", typography: "{typography.body}", height: "{sizing.control-h}" }
  num-input:      { backgroundColor: "{colors_alpha.input-bg}", border: "1px solid {colors_alpha.border}", rounded: "{rounded.md}", typography: "{typography.body}", height: "{sizing.control-h}" }
  range:          { trackColor: "{colors_alpha.border}", thumbFill: "{colors.neutral}", thumbBorder: "1px solid {colors.primary}", rounded: "{rounded.full}" }
---

# Mono UI Style Kit

## Zasada

To jest **kit stylowania**, nie layout. Nie mówi gdzie ma stać sidebar, panel czy kolumna — mówi **jak ma wyglądać** dowolny element wewnątrz istniejącego układu: kolor, typografia, kształt, obramowanie, stany hover/focus/active. Nakładasz to na gotowy szkielet UI (sidebar, panel, toolbar — cokolwiek już masz) bez zmiany jego rozmieszczenia.

Monochromatyczne, tylko tryb ciemny. Jedyne dwa "twarde" kolory to biały (`--primary-color`) i czarny (`--bg-color`) — cała reszta to biały w różnych alfa. Jedyny akcent interakcji to **inwersja**: aktywny/wybrany element odwraca się w biały fill + czarna treść.

## Kolory

| Token | Wartość | Rola |
|---|---|---|
| `--primary-color` | `#FFFFFF` | cały tekst, aktywne wypełnienia, obramowania — 21:1 |
| `--bg-color` | `#000000` | tło, wypełnienie opcji, kciuk/gałka |
| `--secondary-color` | biały 70% | tekst drugorzędny, etykiety, linki |
| `--border-color` | biały 30% | domyślne obramowanie kontrolek |
| obramowanie powierzchni | biały 16% | krawędź "szklanej" powierzchni |
| `--divider-color` | biały 10% | separatory sekcji |
| hover segmentu | biały 8% | hover nieaktywnego przycisku |
| tor scrollbara | biały 5% | tło scrollbara |
| `--input-bg` | czarny 50% | tło "wpuszczonych" kontrolek |
| tło powierzchni | czarny 12% | tło pod blur |

**Aktywne = inwersja.** Brak koloru akcentu dla stanu wybranego — kontrolka odwraca się do biały-fill/czarna-treść (pigułka segmentu, przycisk główny, gałka toggle).

## Typografia

Jedna rodzina — **Inter**, trzy rozmiary: 16 / 12 / 11. Hierarchię poniżej tytułu buduje rozmiar i alfa bieli, **nigdy nowy rozmiar**.

- **Title** 16/500 — tytuł/nagłówek najwyższego poziomu.
- **Body** 12/400 — każda etykieta interaktywna, wartość, select, pole hex, etykieta przycisku/segmentu.
- **Section label** 11/400, UPPERCASE, +0.5px — nagłówki sekcji.
- **Meta** 11/400, +0.5px — linki, drobny tekst.

> ⚠ Przyciski mają `font-weight: 700`, ale jeśli font ładujesz tylko w wagach 400/500, przeglądarka zrobi **faux-bold**. Albo dogrywasz wagę 700 z Google Fonts, albo ustawiasz przycisk na 500.

## Kształty

Miękko-prostokątne, nie pigułkowe. **6px** dla kontenerów (powierzchnia, select, color-/save-control, chassis segmentu, num-input), **3px** dla akcji (przyciski, pigułka i przyciski segmentu), **2px** dla wnętrza swatcha, **pełny promień** tylko dla elementów binarnych/przeciąganych (tor toggle, kciuk slidera, gałka toggle). Kontenery są zawsze łagodniejsze niż akcje w środku.

## Głębia

Tylko blur + krawędź, bez cieni na pojedynczych elementach. Powierzchnia "szklana" (`surface-bg` + `blur(5px)` + 1px `border-panel` + jeden ambient shadow `0 8px 32px`) to jedyna podniesiona warstwa. Kontrolki wewnątrz są "wpuszczone" (`input-bg` + 1px krawędź). Aktywne kontrolki **odwracają się**, nie unoszą. Żadnych cieni per-element, żadnego hover-lift.

---

# Fundamenty (wklej najpierw)

### Import fontu (w `<head>`)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500&display=swap" rel="stylesheet">
```

### Zmienne + reset
```css
:root {
  --bg-color: #000000;
  --primary-color: #ffffff;
  --secondary-color: rgba(255, 255, 255, 0.7);
  --border-color: rgba(255, 255, 255, 0.3);
  --divider-color: rgba(255, 255, 255, 0.1);
  --input-bg: rgba(0, 0, 0, 0.5);
  --border-radius: 6px;
}

* { box-sizing: border-box; }

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  background: var(--bg-color);
  color: var(--primary-color);
}
```

---

# Komponenty (styl, bez pozycjonowania)

Każdy blok CSS opisuje **wygląd elementu w miejscu, gdzie już się znajduje** w Twoim layoucie. Nie ma tu `position`, `top/right/left`, sztywnych szerokości viewportu ani breakpointów układu — jeśli chcesz ograniczyć szerokość konkretnego komponentu (np. selecta), zrób to lokalnie w miejscu użycia.

### Powierzchnia "szklana" (panel / karta / sidebar — tylko styl)
```css
.surface {
  background: rgba(1, 1, 1, 0.12);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border-radius: var(--border-radius);
  padding: 16px;
  color: var(--primary-color);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.16);
}
/* opcjonalny scrollbar wewnętrzny — dodaj gdy .surface ma overflow-y: auto */
.surface::-webkit-scrollbar { width: 8px; }
.surface::-webkit-scrollbar-track { background: rgba(255, 255, 255, 0.05); border-radius: var(--border-radius); }
.surface::-webkit-scrollbar-thumb { background: var(--secondary-color); border-radius: var(--border-radius); }
.surface::-webkit-scrollbar-thumb:hover { background: var(--primary-color); }
```

### Tytuł
```css
.title {
  font-size: 16px;
  font-weight: 500;
  padding-bottom: 16px;
  border-bottom: 1px solid var(--divider-color);
}
```

### Sekcja + nagłówek sekcji + link reset
```css
.section {
  display: flex; flex-direction: column; gap: 4px;
  padding: 8px 0 16px;
  border-bottom: 1px solid var(--divider-color);
}
.section:last-of-type { border-bottom: none; padding-bottom: 0; }

.section-header { display: flex; justify-content: space-between; align-items: center; height: 32px; }
.section-title { font-size: 11px; text-transform: uppercase; letter-spacing: 0.5px; }

.reset-btn { font-size: 11px; color: var(--secondary-color); cursor: pointer; text-decoration: none; transition: color 0.2s ease; }
.reset-btn:hover { color: var(--primary-color); }
```

### Wiersz kontrolki + etykieta + stan disabled
```css
.row { display: flex; align-items: center; gap: 8px; min-height: 32px; }
.row-label { flex-shrink: 0; font-size: 12px; color: var(--secondary-color); line-height: 24px; }
.row.disabled { opacity: 0.35; pointer-events: none; }
.row input[type="range"] { flex: 1; min-width: 0; }
```

### Input numeryczny
```css
.num-input {
  width: 32px; height: 32px; flex-shrink: 0;
  background: var(--input-bg);
  border: 1px solid var(--border-color);
  border-radius: var(--border-radius);
  color: var(--primary-color);
  font-family: 'Inter', sans-serif; font-size: 12px;
  text-align: center; padding: 0; outline: none;
  transition: border-color 0.2s ease;
}
.num-input:focus { border-color: var(--primary-color); }
.num-input::-webkit-inner-spin-button,
.num-input::-webkit-outer-spin-button { -webkit-appearance: none; margin: 0; }
.num-input[type="number"] { -moz-appearance: textfield; }
```

### Suwak (range)
```css
input[type="range"] { height: 32px; background: transparent; outline: none; -webkit-appearance: none; cursor: pointer; }

input[type="range"]::-webkit-slider-runnable-track { height: 1px; background: var(--border-color); }
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none; appearance: none;
  width: 14px; height: 14px; margin-top: -6.5px;
  border-radius: 50%; background: #000000; border: 1px solid #ffffff;
  cursor: pointer; transition: transform 0.15s ease;
}
input[type="range"]::-webkit-slider-thumb:hover { transform: scale(1.25); }
input[type="range"]:active::-webkit-slider-thumb { transform: scale(1.15); }

input[type="range"]::-moz-range-track { height: 1px; background: var(--border-color); }
input[type="range"]::-moz-range-thumb {
  width: 12px; height: 12px; border-radius: 50%;
  background: #000000; border: 1px solid #ffffff;
  cursor: pointer; transition: transform 0.15s ease;
}
input[type="range"]::-moz-range-thumb:hover { transform: scale(1.25); }
```

### Kontrolka koloru (swatch + hex + clear)
```css
.color-control {
  height: 32px;
  display: flex; align-items: center; gap: 8px;
  padding: 0 8px 0 4px;
  background: var(--input-bg);
  border: 1px solid var(--border-color);
  border-radius: var(--border-radius);
}
input[type="color"] {
  width: 24px; height: 24px; flex-shrink: 0;
  border: 1px solid var(--border-color); border-radius: 3px;
  cursor: pointer; background: transparent; overflow: hidden; padding: 0;
  -webkit-appearance: none;
}
input[type="color"]::-webkit-color-swatch-wrapper { padding: 0; }
input[type="color"]::-webkit-color-swatch { border: none; border-radius: 2px; }
input[type="color"]::-moz-color-swatch { border: none; border-radius: 2px; }

.color-hex {
  flex: 1; min-width: 0; background: transparent; border: none;
  color: var(--primary-color); font-family: 'Inter', sans-serif; font-size: 12px;
  text-transform: uppercase; outline: none; padding: 0;
}
.color-clear {
  width: 20px; height: 20px; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center;
  color: var(--primary-color); font-size: 12px; line-height: 1;
  cursor: pointer; opacity: 0.7;
  transition: opacity 0.2s ease, transform 0.15s ease; user-select: none;
}
.color-clear:hover { opacity: 1; transform: scale(1.2); }
.row.off input[type="color"], .row.off .color-hex { opacity: 0.3; }
```

### Toggle (przełącznik)
```css
.toggle {
  position: relative; width: 32px; height: 22px; flex-shrink: 0;
  display: flex; align-items: center; padding: 4px;
  background: var(--input-bg);
  border: 1px solid var(--border-color);
  border-radius: 9999px; cursor: pointer;
  transition: border-color 0.2s ease;
}
.toggle:hover { border-color: var(--primary-color); }
.toggle input { position: absolute; opacity: 0; width: 0; height: 0; }
.toggle .knob {
  width: 12px; height: 12px; border-radius: 50%;
  background: #000000; border: 1px solid var(--border-color); box-sizing: border-box;
  transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1), border-color 0.25s ease;
}
.toggle:hover .knob { transform: scale(1.15); }
.toggle input:checked + .knob { border-color: #ffffff; transform: translateX(10px); }
.toggle:hover input:checked + .knob { transform: translateX(10px) scale(1.15); }
```

### Przycisk (akcja główna) + rząd przycisków
```css
button {
  background: var(--primary-color);
  color: #000000;
  border: none; border-radius: 3px;
  font-family: 'Inter', sans-serif; font-size: 12px;
  cursor: pointer; text-align: center;
  transition: opacity 0.2s ease, transform 0.1s ease;
}
button:hover { opacity: 0.85; }
button:active { transform: scale(0.96); }

.button-row { display: flex; gap: 8px; }
.button-row button { flex: 1; height: 32px; font-weight: 700; padding: 0 8px; }
```

### Select (rozwijana lista)
```css
select {
  height: 32px; flex-shrink: 0;
  padding: 0 28px 0 8px;
  background: var(--input-bg); color: var(--primary-color);
  border: 1px solid var(--border-color); border-radius: var(--border-radius);
  font-family: 'Inter', sans-serif; font-size: 12px;
  cursor: pointer; outline: none; transition: border-color 0.2s ease;
  -webkit-appearance: none; -moz-appearance: none; appearance: none;
  background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg width='10' height='6' viewBox='0 0 10 6' fill='none' xmlns='http://www.w3.org/2000/svg'%3e%3cpath d='M1 1L5 5L9 1' stroke='white' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3e%3c/svg%3e");
  background-repeat: no-repeat; background-position: right 8px center;
}
select:hover, select:focus { border-color: var(--primary-color); }
select option { background: #000000; color: var(--primary-color); padding: 8px; }
```

### Segmented control (przesuwana pigułka)
```css
.segmented {
  position: relative; display: flex; align-items: center;
  width: 100%; height: 32px; padding: 0 4px;
  background: var(--input-bg); border: 1px solid var(--border-color);
  border-radius: var(--border-radius);
}
.seg-pill {
  position: absolute; left: 4px; top: 3px;
  width: calc(50% - 4px); height: 24px;
  background: var(--primary-color); border-radius: 3px;
  transition: transform 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}
.segmented[data-active="option-2"] .seg-pill { transform: translateX(100%); }
.segmented button {
  position: relative; z-index: 1; flex: 1; height: 24px;
  background: transparent; color: var(--primary-color); border-radius: 3px;
  font-size: 12px; padding: 0 8px;
  transition: color 0.25s ease, background 0.2s ease;
}
.segmented button:hover { background: rgba(255, 255, 255, 0.08); }
.segmented button.active { color: #000000; background: transparent; }
.segmented button.active:hover { background: transparent; }
```
> Dla >2 opcji: poszerz `.seg-pill` do `calc(100%/N - ...)` i przesuwaj wg indeksu aktywnej opcji.

### Pole zapisu (input + przycisk inline)
```css
.save-control {
  height: 32px;
  display: flex; align-items: center; gap: 8px;
  padding: 0 4px 0 8px;
  background: var(--input-bg); border: 1px solid var(--border-color);
  border-radius: var(--border-radius); transition: border-color 0.2s ease;
}
.save-control:focus-within { border-color: var(--primary-color); }
.save-control input[type="text"] {
  flex: 1; min-width: 0; background: transparent; border: none;
  color: var(--primary-color); font-family: 'Inter', sans-serif; font-size: 12px;
  outline: none; padding: 0;
}
.save-control input[type="text"]::placeholder { color: rgba(255, 255, 255, 0.3); }
.save-control button { height: 24px; padding: 0 8px; flex-shrink: 0; }
```

### Tekst pomocniczy / link (styl, bez pozycji)
```css
.hint { color: rgba(255, 255, 255, 0.35); font-size: 11px; }
.link { color: var(--secondary-color); font-size: 11px; letter-spacing: 0.5px; text-decoration: none; }
.link strong, .link a { color: var(--primary-color); font-weight: 500; }
.link a:hover { opacity: 0.7; }
```

---

## Przejścia i mikroanimacje

| Właściwość | Czas / easing | Gdzie |
|---|---|---|
| `border-color`, `color`, `opacity` | `0.2s ease` | inputy, selecty, przyciski, linki |
| `transform` (naciśnięcie) | `0.1s ease` | `button:active` (scale 0.96) |
| `transform` (skala kciuka/gałki) | `0.15s ease` | kciuk slidera (1.25/1.15×), clear (1.2×) |
| przesunięcie pigułki/gałki | `0.25s cubic-bezier(0.4, 0, 0.2, 1)` | pigułka segmentu, gałka toggle |
| `color` na etykiecie segmentu | `0.25s ease` | zmiana koloru tekstu przy aktywacji |

## Do / Don't

**Rób tak**
- Trzymaj UI **monochromatyczne** — kolor należy do treści/danych, nie do chrome'u.
- Buduj hierarchię z **rampy alfa bieli** i 1px krawędzi; zanim wymyślisz nową wartość, sprawdź czy pasuje istniejący stopień rampy.
- Sygnalizuj aktywność przez **inwersję** (biały fill / czarna treść) — pigułka segmentu, przycisk główny, gałka toggle.
- Trzymaj się trzech rozmiarów typografii (16/12/11) i wysokości kontrolki 32px.
- Kontrolki mają być "wpuszczone" (`--input-bg`); podniesienie (blur + cień) zarezerwuj dla powierzchni.

**Nie rób tak**
- Nie wprowadzaj koloru marki/akcentu ani jasnego trybu bez świadomej decyzji — to zmienia charakter systemu.
- Nie dodawaj cieni na pojedynczych kontrolkach — jeden ambient shadow żyje na powierzchni.
- Nie rozmieszczaj tego pliku jako layoutu — nie ma tu `position`, sztywnych offsetów viewportu ani breakpointów układu. To warstwa stylu nakładana na istniejący szkielet.
- Nie zostawiaj cichego faux-bold na przyciskach — dogrywaj wagę 700 albo ustaw 500.

---

## Rozszerzanie standardu

Ten plik jest **jedynym źródłem prawdy** dla stylu i spójności UI — nowe komponenty, nowe warianty i wyjątki mają tu trafiać, a nie żyć rozproszone po kodzie.

Jeśli podczas pracy trafisz na element, którego ten dokument nie opisuje (np. modal, tabela, tooltip, badge, wykres, empty state):

1. **Nie wymyślaj nowego stylu w locie.** Wyprowadź propozycję z istniejących zasad (paleta, rampa alfy, 3 rozmiary typografii, promienie, jedna głębia, inwersja jako sygnał aktywności).
2. **Zapytaj / zaproponuj przed wdrożeniem** — zwłaszcza gdy nie jest oczywiste, jak zmapować element na istniejące tokeny.
3. Po zatwierdzeniu — **dopisz ustalenie do tego pliku** (nowa pozycja w `components:` we frontmatterze + odpowiadająca jej sekcja CSS w części "Komponenty"), zamiast trzymać wyjątek tylko w kodzie. Dzięki temu `DESIGN.MD` zawsze odzwierciedla pełny, aktualny standard, a kolejne zmiany w UI mają się o co oprzeć.
