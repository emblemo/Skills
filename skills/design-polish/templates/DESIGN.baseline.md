---
version: alpha
name: Mono UI Style Kit
description: A universal, monochrome component styling system (dark-only). Contains no layout or positioning — it covers only the LOOK of elements (color, typography, shape, borders, states). Applied on top of an existing panel/sidebar layout without changing where anything sits.

# ⚠ STATUS: STANDARD / SOURCE OF TRUTH
# This file is the single source of truth for the look and consistency of the
# project's UI. Every styling decision (color, typography, shape, shadow,
# interaction state) must be traceable back to this file. If something isn't
# covered here yet — see "Extending the standard" at the end of this document
# before introducing anything new.

colors:
  primary: "#FFFFFF"      # Ink White — all text, active fills, slider/knob borders, button fill
  neutral: "#000000"      # Canvas Black — background, option fill, slider-thumb & toggle-knob fill
  on-primary: "#000000"   # content on a white fill (button label, active segmented label) — 21:1 contrast

colors_alpha:
  secondary:     "rgba(255,255,255,0.70)"  # secondary text, labels, reset links, scrollbar thumb
  border:        "rgba(255,255,255,0.30)"  # default control border, slider track, placeholder
  border-panel:  "rgba(255,255,255,0.16)"  # border of a "glass" surface
  divider:       "rgba(255,255,255,0.10)"  # section dividers / separators
  hover-plate:   "rgba(255,255,255,0.08)"  # hover on an inactive segmented-control button
  track-faint:   "rgba(255,255,255,0.05)"  # scrollbar track
  credit-faint:  "rgba(255,255,255,0.35)"  # helper text / disabled note
  input-bg:      "rgba(0,0,0,0.50)"        # recessed fill behind interactive controls
  surface-bg:    "rgba(1,1,1,0.12)"        # fill of a "glass" surface (under blur)

shadows:
  ambient: "rgba(0,0,0,0.40)"   # the only shadow in the system — box-shadow: 0 8px 32px {shadows.ambient}

effects:
  surface-blur: "blur(5px)"     # backdrop-filter on "glass" surfaces

typography:
  title:          # heading / panel title
    fontFamily: Inter
    fontSize: 16px
    fontWeight: 500
    lineHeight: 1.2
  section-label:  # section header labels
    fontFamily: Inter
    fontSize: 11px
    fontWeight: 400
    letterSpacing: 0.5px
    textTransform: uppercase
  body:           # control labels, values, select/hex text, button labels
    fontFamily: Inter
    fontSize: 12px
    fontWeight: 400
  meta:           # links, footers, small helper text
    fontFamily: Inter
    fontSize: 11px
    fontWeight: 400
    letterSpacing: 0.5px
  button:         # primary action buttons
    fontFamily: Inter
    fontSize: 12px
    fontWeight: 700   # ⚠ see the note in the Typography section

rounded:
  xs: 2px       # smallest elements (e.g. inside a color swatch)
  sm: 3px       # buttons, segmented-control pill
  md: 6px       # standard radius for controls and surfaces
  full: 9999px  # binary/draggable elements (toggle, slider thumb)

sizing:
  control-h: 32px     # canonical control height
  unit: 4px           # base spacing unit inside a component (4 / 8 / 16)

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

## Principle

This is a **styling kit**, not a layout. It doesn't say where a sidebar, panel, or column should sit — it says **how any element should look** inside an existing layout: color, typography, shape, border, hover/focus/active states. You apply it on top of whatever UI skeleton already exists (sidebar, panel, toolbar — anything) without changing its arrangement.

Monochrome, dark mode only. The only two "hard" colors are white (`--primary-color`) and black (`--bg-color`) — everything else is white at various alpha levels. The single interaction accent is **inversion**: an active/selected element flips to a white fill with black content.

## Colors

| Token | Value | Role |
|---|---|---|
| `--primary-color` | `#FFFFFF` | all text, active fills, borders — 21:1 |
| `--bg-color` | `#000000` | background, option fill, thumb/knob |
| `--secondary-color` | white 70% | secondary text, labels, links |
| `--border-color` | white 30% | default control border |
| surface border | white 16% | edge of a "glass" surface |
| `--divider-color` | white 10% | section separators |
| segmented hover | white 8% | hover on an inactive button |
| scrollbar track | white 5% | scrollbar background |
| `--input-bg` | black 50% | fill of "recessed" controls |
| surface fill | black 12% | fill under the blur |

**Active = inversion.** No accent color for the selected state — the control flips to a white-fill/black-content look (segmented pill, primary button, toggle knob).

## Typography

One family — **Inter**, three sizes: 16 / 12 / 11. Hierarchy below the title comes from size and white-alpha, **never a new size**.

- **Title** 16/500 — top-level heading/title.
- **Body** 12/400 — every interactive label, value, select, hex field, button/segmented label.
- **Section label** 11/400, UPPERCASE, +0.5px — section headers.
- **Meta** 11/400, +0.5px — links, small text.

> ⚠ Buttons use `font-weight: 700`, but if you only load the font in weights 400/500, the browser will **faux-bold** it. Either add weight 700 from Google Fonts, or set the button to 500.

## Shapes

Soft-rectangular, not pill-shaped. **6px** for containers (surface, select, color-/save-control, segmented chassis, num-input), **3px** for actions (buttons, segmented pill and buttons), **2px** for a swatch's inner corner, **full radius** only for binary/draggable elements (toggle track, slider thumb, toggle knob). Containers are always softer than the actions inside them.

## Depth

Blur + edge only, no shadows on individual elements. The "glass" surface (`surface-bg` + `blur(5px)` + 1px `border-panel` + one ambient shadow `0 8px 32px`) is the only elevated layer. Controls inside it are "recessed" (`input-bg` + 1px border). Active controls **invert**, they don't lift. No per-element shadows, no hover-lift.

---

# Foundations (paste first)

### Font import (in `<head>`)
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500&display=swap" rel="stylesheet">
```

### Variables + reset
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

# Components (style only, no positioning)

Every CSS block below describes **how an element should look wherever it already sits** in your layout. There's no `position`, no `top/right/left`, no hardcoded viewport widths or layout breakpoints — if you want to constrain the width of a specific component (e.g. a select), do it locally at its usage site.

### "Glass" surface (panel / card / sidebar — style only)
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
/* optional internal scrollbar — add when .surface has overflow-y: auto */
.surface::-webkit-scrollbar { width: 8px; }
.surface::-webkit-scrollbar-track { background: rgba(255, 255, 255, 0.05); border-radius: var(--border-radius); }
.surface::-webkit-scrollbar-thumb { background: var(--secondary-color); border-radius: var(--border-radius); }
.surface::-webkit-scrollbar-thumb:hover { background: var(--primary-color); }
```

### Title
```css
.title {
  font-size: 16px;
  font-weight: 500;
  padding-bottom: 16px;
  border-bottom: 1px solid var(--divider-color);
}
```

### Section + section header + reset link
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

### Control row + label + disabled state
```css
.row { display: flex; align-items: center; gap: 8px; min-height: 32px; }
.row-label { flex-shrink: 0; font-size: 12px; color: var(--secondary-color); line-height: 24px; }
.row.disabled { opacity: 0.35; pointer-events: none; }
.row input[type="range"] { flex: 1; min-width: 0; }
```

### Numeric input
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

### Range slider
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

### Color control (swatch + hex + clear)
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

### Toggle switch
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

### Button (primary action) + button row
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

### Select (dropdown)
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

### Segmented control (sliding pill)
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
> For >2 options: widen `.seg-pill` to `calc(100%/N - ...)` and translate it based on the active index.

### Save control (input + inline button)
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

### Helper text / link (style only, no positioning)
```css
.hint { color: rgba(255, 255, 255, 0.35); font-size: 11px; }
.link { color: var(--secondary-color); font-size: 11px; letter-spacing: 0.5px; text-decoration: none; }
.link strong, .link a { color: var(--primary-color); font-weight: 500; }
.link a:hover { opacity: 0.7; }
```

---

## Transitions & motion

| Property | Duration / easing | Where |
|---|---|---|
| `border-color`, `color`, `opacity` | `0.2s ease` | inputs, selects, buttons, links |
| `transform` (press) | `0.1s ease` | `button:active` (scale 0.96) |
| `transform` (thumb/knob scale) | `0.15s ease` | slider thumb (1.25/1.15×), clear (1.2×) |
| pill/knob travel | `0.25s cubic-bezier(0.4, 0, 0.2, 1)` | segmented pill, toggle knob |
| `color` on segmented label | `0.25s ease` | text color flip on activation |

## Do's and Don'ts

**Do**
- Keep the UI **monochrome** — color belongs to content/data, not chrome.
- Build hierarchy from the **white-alpha ramp** and 1px borders; before inventing a new value, check whether an existing ramp step already fits.
- Signal active/selected state via **inversion** (white fill / black content) — segmented pill, primary button, toggle knob.
- Hold to the three type sizes (16/12/11) and the 32px control height for new controls.
- Keep controls "recessed" on `--input-bg`; reserve elevation for the surface alone.

**Don't**
- Don't introduce a brand/accent color or a light mode without a deliberate decision — it changes the character of the system.
- Don't add shadows on individual controls — the single ambient shadow lives on the surface only.
- Don't lay this file out as a layout spec — there's no `position`, no hardcoded viewport offsets, no layout breakpoints here. This is a styling layer applied on top of an existing skeleton.
- Don't ship silent faux-bold on buttons — load weight 700, or set it to 500.

---

## Extending the standard

This file is the **single source of truth** for the look and consistency of the UI — new components, new variants, and exceptions belong here, not scattered across the code.

If you run into an element this document doesn't describe (e.g. modal, table, tooltip, badge, chart, empty state):

1. **Don't invent a new style on the fly.** Derive a proposal from the existing rules (palette, alpha ramp, the three typography sizes, radii, single depth, inversion as the activity signal).
2. **Ask / propose before implementing** — especially when it's not obvious how to map the element onto existing tokens.
3. Once approved — **add the decision to this file** (a new entry in `components:` in the frontmatter + the matching CSS section under "Components"), instead of keeping the exception only in the code. That way `DESIGN.MD` always reflects the full, current standard, and future UI changes have something solid to build on.
